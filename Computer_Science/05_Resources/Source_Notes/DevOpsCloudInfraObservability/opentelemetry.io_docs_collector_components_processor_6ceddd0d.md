Title: Processors | OpenTelemetry
Mapped Topic: Traces, metrics, logs, instrumentation
Source URL: https://opentelemetry.io/docs/collector/components/processor/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:11:59+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

Processors List of available OpenTelemetry Collector processors

Processors transform, filter, and enrich telemetry data as it flows through the
pipeline. For more information on how to configure processors, see the
Collector configuration documentation .

Name Distributions Traces Metrics Logs Attributes Processor contrib, core, K8s beta beta beta Batch Processor contrib, core, K8s beta beta beta Coralogix Processor contrib alpha - - Cumulative to Delta Processor contrib, K8s - beta - Delta to Cumulative Processor contrib, K8s - alpha - Delta to Rate Processor contrib, K8s - alpha - DNS Lookup Processor contrib development development development Filter Processor contrib, core, K8s alpha alpha alpha GeoIP Processor contrib alpha alpha alpha Group by Attributes Processor contrib, K8s beta beta beta Group by Trace Processor contrib, K8s beta - - Interval Processor contrib, K8s - alpha - Isolation Forest Processor contrib alpha alpha alpha Kubernetes Attributes Processor contrib, K8s beta beta beta Log DeDuplication Processor contrib, K8s - - alpha Logs Transform Processor contrib - - development Lookup Processor contrib - - development Memory Limiter Processor contrib, core, K8s beta beta beta Metrics Generation Processor contrib - alpha - Metric Start Time Processor contrib - beta - Metrics Transform Processor contrib, K8s - beta - Probabilistic Sampling Processor contrib, core, K8s beta - alpha Redaction Processor contrib, K8s beta alpha alpha Remote Tap Processor contrib, K8s alpha alpha alpha Resource Detection Processor contrib, K8s beta beta beta Resource Processor contrib, core, K8s beta beta beta Schema Processor contrib development development development Span Processor contrib, core alpha - - spanpruningprocessor contrib alpha - - Sumo Logic Processor contrib beta beta beta Tail Sampling Processor contrib, K8s beta - - Transform Processor contrib, K8s beta beta beta Unroll Processor contrib - - alpha

Feedback Was this page helpful?

Yes
No Thank you. Your feedback is appreciated!

Please let us know how we can improve this page . Your feedback is appreciated!
