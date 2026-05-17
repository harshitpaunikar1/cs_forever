Title: No Collector | OpenTelemetry
Mapped Topic: Traces, metrics, logs, instrumentation
Source URL: https://opentelemetry.io/docs/collector/deploy/other/no-collector/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:12:09+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

Send signals directly from an application to backends

The most direct deployment pattern doesn’t use a Collector at all. In this
approach, applications instrumented with an OpenTelemetry SDK
export telemetry signals (traces, metrics, and logs) straight to a backend:

Example

See the instrumentation documentation for end-to-end examples
that show how to export signals directly from your application to a backend.

Trade-offs

Here are the key pros and cons of skipping the Collector:

Pros:

Straightforward to use, especially in development and test environments

No additional moving parts to deploy or operate

Cons:

Requires code changes if collection, processing, or ingestion needs change

Strong coupling between application code and backend storage or visualization

Each language implementation supports only a limited number of exporters
