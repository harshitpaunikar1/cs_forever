Title: Deploy the Collector | OpenTelemetry
Mapped Topic: Traces, metrics, logs, instrumentation
Source URL: https://opentelemetry.io/docs/collector/deploy/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:12:03+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

[Agent deployment pattern](https://opentelemetry.io/docs/collector/deploy/agent/)

Send signals to Collectors and then export to backends

Patterns you can apply to deploy the OpenTelemetry Collector

The OpenTelemetry Collector consists of a single binary that you can deploy in
different ways for different use cases. This section describes common deployment
patterns, their use cases, and pros and cons. It also provides best practices
for configuring the Collector in cross-environment and multi-backend scenarios.
For deployment-related security considerations, see the [Collector hosting best
practices](https://opentelemetry.io/docs/security/hosting-best-practices/).

- KubeCon NA 2021 talk on
[OpenTelemetry Collector Deployment Patterns](https://www.youtube.com/watch?v=WhRrwSHDBFs)[Deployment patterns](https://github.com/jpkrohling/opentelemetry-collector-deployment-patterns/)accompanying the talk

Send signals to Collectors and then export to backends

Learn why and how to send signals first to a single OTLP endpoint and then to backends

Was this page helpful?

Thank you. Your feedback is appreciated!

Please let us know [how we can improve this page](https://github.com/open-telemetry/opentelemetry.io/issues/new?template=PAGE_FEEDBACK.yml&title=[Page+feedback]%3A+ADD+A+SUMMARY+OF+YOUR+FEEDBACK+HERE). Your feedback is appreciated!
