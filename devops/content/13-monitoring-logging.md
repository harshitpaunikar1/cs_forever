# Monitoring & Logging

You cannot improve what you cannot observe. The three pillars of observability —
metrics, logs, and traces — give you the visibility needed to understand system
health, diagnose failures, and make informed decisions about your infrastructure.

---

## The Three Pillars of Observability

| Pillar | What it answers | Tools |
|--------|----------------|-------|
| **Metrics** | Is it working? How fast? How many? | Prometheus, Grafana, CloudWatch |
| **Logs** | What happened? Why? | Loki, ELK, Fluentd |
| **Traces** | Where is the slowness? Which service? | Jaeger, Tempo, Zipkin |

**SLI / SLO / SLA**:
- **SLI** (Service Level Indicator): a metric you actually measure (e.g., % of requests < 200ms)
- **SLO** (Service Level Objective): target for an SLI (e.g., 99.9% of requests < 200ms)
- **SLA** (Service Level Agreement): contractual commitment to customers; SLA ≤ SLO

**Error budget**: `1 - SLO`. If SLO = 99.9%, you have 0.1% of time (43 minutes/month) to be
non-compliant. Burn through your error budget → freeze risky changes.

---

## Prometheus

Prometheus is the standard metrics system for cloud-native applications.
It scrapes (pulls) metrics from targets on a schedule.

### Architecture

```
Applications  ─────────►  Prometheus Server  ────►  Alertmanager  ───►  Slack/PD
Exporters     ─────────►  (scrape every 15s)  │
                                               └────►  Grafana (query & visualize)
```

### Data Model

Every time series is identified by a metric name and a set of labels:

```
http_requests_total{job="api", method="GET", status="200"}  1234
http_requests_total{job="api", method="POST", status="500"}  12
```

### Metric Types

| Type | Description | Use case |
|------|-------------|---------|
| **Counter** | Only goes up; reset on restart | Request count, error count |
| **Gauge** | Can go up or down | Current connections, memory usage |
| **Histogram** | Samples observations into buckets | Request latency, response size |
| **Summary** | Client-side quantiles | Latency percentiles (less flexible) |

### prometheus.yml

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "rules/*.yml"

alerting:
  alertmanagers:
    - static_configs:
        - targets: ["alertmanager:9093"]

scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: node
    static_configs:
      - targets: ["node1:9100", "node2:9100", "node3:9100"]

  - job_name: kubernetes-pods
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: "true"
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
```

### PromQL

```promql
# Current value of a metric
up

# Counter rate (per-second rate over last 5 minutes)
rate(http_requests_total[5m])

# Increase over a window
increase(http_requests_total[1h])

# Filter by label
rate(http_requests_total{job="api", status=~"5.."}[5m])

# Aggregate across labels
sum(rate(http_requests_total[5m]))
sum by (status) (rate(http_requests_total[5m]))
sum without (instance) (rate(http_requests_total[5m]))

# Top 5 by value
topk(5, rate(http_requests_total[5m]))

# Histogram quantiles (p99 latency)
histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))

# Comparison
rate(http_requests_total{status=~"5.."}[5m]) / rate(http_requests_total[5m]) > 0.01

# CPU usage
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

# Memory available
node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes * 100
```

### Recording and Alerting Rules

```yaml
# rules/api.yml
groups:
  - name: api_rules
    interval: 30s
    rules:
      # Recording rule: pre-compute expensive query
      - record: job:http_requests:rate5m
        expr: sum by (job) (rate(http_requests_total[5m]))

      # Alert: high error rate
      - alert: HighErrorRate
        expr: |
          sum by (job) (rate(http_requests_total{status=~"5.."}[5m]))
          /
          sum by (job) (rate(http_requests_total[5m]))
          > 0.05
        for: 2m         # Must be true for 2 minutes before firing
        labels:
          severity: critical
        annotations:
          summary: "High error rate for {{ $labels.job }}"
          description: "Error rate is {{ $value | humanizePercentage }}"
          runbook_url: "https://wiki.example.com/runbooks/high-error-rate"

      # Alert: instance down
      - alert: InstanceDown
        expr: up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Instance {{ $labels.instance }} is down"
```

### Alertmanager

```yaml
# alertmanager.yml
route:
  group_by: [alertname, job]
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 4h
  receiver: default
  routes:
    - match:
        severity: critical
      receiver: pagerduty
    - match:
        severity: warning
      receiver: slack

receivers:
  - name: default
    slack_configs:
      - api_url: "https://hooks.slack.com/services/..."
        channel: "#alerts"
        title: "[{{ .Status | upper }}] {{ .GroupLabels.alertname }}"
        text: "{{ range .Alerts }}{{ .Annotations.description }}\n{{ end }}"

  - name: pagerduty
    pagerduty_configs:
      - routing_key: "your-pagerduty-integration-key"
        severity: '{{ if eq .GroupLabels.severity "critical" }}critical{{ else }}warning{{ end }}'

inhibit_rules:
  - source_match:
      alertname: InstanceDown
    target_match:
      alertname: HighErrorRate
    equal: [instance]   # If an instance is down, suppress its high error rate alert
```

---

## Grafana

Grafana visualizes metrics from Prometheus, Loki, CloudWatch, and many other sources.

### Key Concepts

- **Dashboard**: collection of panels
- **Panel**: single visualization (graph, gauge, table, stat, etc.)
- **Variable**: template variable for filtering (e.g., `$job`, `$instance`)
- **Data source**: connection to a metrics/logs backend

### Example Dashboard Query

```promql
# CPU usage panel
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle", instance=~"$instance"}[5m])) * 100)

# Request rate
sum(rate(http_requests_total{job=~"$job"}[5m]))

# p99 latency
histogram_quantile(0.99, sum by (le, job) (rate(http_request_duration_seconds_bucket{job=~"$job"}[5m])))
```

### Provisioning (Dashboards as Code)

```yaml
# /etc/grafana/provisioning/datasources/prometheus.yml
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    url: http://prometheus:9090
    isDefault: true

# /etc/grafana/provisioning/dashboards/default.yml
apiVersion: 1
providers:
  - name: Default
    folder: DevOps
    type: file
    options:
      path: /var/lib/grafana/dashboards
```

---

## Logging

### Structured Logging

Prefer JSON logs over free-form text. Structured logs are machine-parseable.

```json
{
  "timestamp": "2024-01-15T10:30:00Z",
  "level": "ERROR",
  "service": "payment-api",
  "trace_id": "abc123",
  "user_id": "u-456",
  "message": "Payment processing failed",
  "error": "connection timeout",
  "duration_ms": 5001
}
```

**Log levels** (use consistently):
- `DEBUG`: verbose, development only
- `INFO`: normal operation events
- `WARN`: unexpected but handled situation
- `ERROR`: something failed; needs investigation
- `FATAL`: unrecoverable; application exits

### Loki

Loki is a log aggregation system by Grafana Labs. Unlike Elasticsearch, Loki indexes
only labels (not the log content), making it much more cost-effective.

```yaml
# docker-compose.yml
services:
  loki:
    image: grafana/loki:2.9.0
    ports:
      - "3100:3100"

  promtail:
    image: grafana/promtail:2.9.0
    volumes:
      - /var/log:/var/log
      - ./promtail-config.yml:/etc/promtail/config.yml
```

```yaml
# promtail-config.yml
server:
  http_listen_port: 9080

clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:
  - job_name: system
    static_configs:
      - targets: [localhost]
        labels:
          job: varlogs
          __path__: /var/log/*.log

  - job_name: docker
    docker_sd_configs:
      - host: unix:///var/run/docker.sock
    relabel_configs:
      - source_labels: [__meta_docker_container_name]
        target_label: container
```

**LogQL** (Loki query language):

```logql
# Stream selector (required)
{job="api", environment="production"}

# Filter
{job="api"} |= "ERROR"
{job="api"} != "healthcheck"
{job="api"} | json | level = "error"

# Rate
rate({job="api"}[5m])

# Count errors per service
sum by (service) (count_over_time({environment="production"} |= "ERROR" [5m]))

# Parse JSON and filter
{job="api"} | json | duration_ms > 1000
```

---

## ELK Stack

**Elasticsearch** stores and indexes logs as documents.
**Logstash** ingests, transforms, and ships logs.
**Kibana** visualizes and searches logs.

```
Application logs → Filebeat → Logstash → Elasticsearch → Kibana
```

### Logstash Pipeline

```
# /etc/logstash/conf.d/app.conf
input {
  beats {
    port => 5044
  }
}

filter {
  grok {
    match => { "message" => "%{COMBINEDAPACHELOG}" }
  }
  date {
    match => ["timestamp", "dd/MMM/yyyy:HH:mm:ss Z"]
    target => "@timestamp"
  }
  mutate {
    remove_field => ["message"]
    convert => { "response" => "integer" }
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "access-logs-%{+YYYY.MM.dd}"
  }
}
```

### When to use Loki vs ELK

| | Loki | ELK |
|--|------|-----|
| **Cost** | Low (label-only indexing) | High (full-text indexing) |
| **Query speed** | Slower (scans log content) | Faster (inverted index) |
| **Setup complexity** | Simple | Complex |
| **Best for** | Cloud-native, Kubernetes, Prometheus users | Full-text search, complex queries, compliance |

---

## Distributed Tracing

In microservices, a single user request might touch 10+ services. Distributed tracing
shows the entire call chain and where time is spent.

### Concepts

- **Trace**: full journey of one request through the system
- **Span**: one unit of work within a trace (e.g., a service call, DB query)
- **Context propagation**: passing trace/span IDs in request headers across services
- **W3C TraceContext**: standard headers: `traceparent`, `tracestate`

### OpenTelemetry

OpenTelemetry (OTel) is the standard for instrumentation. It's vendor-neutral.

```python
# Python example
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.exporter.otlp.proto.grpc.trace_exporter import OTLPSpanExporter

provider = TracerProvider()
provider.add_span_processor(
    BatchSpanProcessor(OTLPSpanExporter(endpoint="http://otel-collector:4317"))
)
trace.set_tracer_provider(provider)

tracer = trace.get_tracer("my-service")

def process_order(order_id: str):
    with tracer.start_as_current_span("process-order") as span:
        span.set_attribute("order.id", order_id)
        # ... business logic ...
```

```yaml
# OpenTelemetry Collector config
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317

processors:
  batch:

exporters:
  jaeger:
    endpoint: jaeger:14250
  prometheus:
    endpoint: "0.0.0.0:8889"

service:
  pipelines:
    traces:
      receivers: [otlp]
      processors: [batch]
      exporters: [jaeger]
    metrics:
      receivers: [otlp]
      processors: [batch]
      exporters: [prometheus]
```

---

## Common Exporters (Prometheus)

| Exporter | Metrics |
|----------|---------|
| **node_exporter** | Host CPU, memory, disk, network |
| **blackbox_exporter** | HTTP/TCP/DNS endpoint availability |
| **cadvisor** | Container CPU, memory, disk per container |
| **kube-state-metrics** | Kubernetes object state (pod status, deployment replicas) |
| **postgres_exporter** | PostgreSQL query stats, connections, replication lag |
| **redis_exporter** | Redis memory, commands, keyspace |
| **nginx-prometheus-exporter** | Nginx active connections, requests/s |

---

## On-Call Best Practices

**Runbooks**: for every alert, write a runbook that explains:
1. What triggered this alert
2. What the user impact is
3. How to diagnose (commands to run)
4. How to fix it

**Blameless postmortems**: after an incident, focus on systems and processes, not people.
Document: timeline, root cause, contributing factors, action items.

**Alert fatigue prevention**:
- Every alert should be actionable
- Alerts should fire only when human action is required
- Page for customer-impacting issues only; route the rest to a chat channel
- Tune `for` duration in Prometheus rules to reduce noise from transient issues
- Set up alert inhibition: don't alert for downstream symptoms when you're already paging for the root cause
