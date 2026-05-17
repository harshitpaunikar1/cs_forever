Title: What is OpenTelemetry? | OpenTelemetry
Mapped Topic: Traces, metrics, logs, instrumentation
Source URL: https://opentelemetry.io/docs/what-is-opentelemetry/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:11:46+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

A brief explanation of what OpenTelemetry is and isn’t.

OpenTelemetry is:

An

designed to facilitate the[observability](https://opentelemetry.io/concepts/observability-primer/#what-is-observability)framework and toolkit[Generation](https://opentelemetry.io/concepts/instrumentation)- Export
[Collection](https://opentelemetry.io/concepts/components/#collector)

of

[telemetry data](https://opentelemetry.io/concepts/signals/)such as[traces](https://opentelemetry.io/concepts/signals/traces/),[metrics](https://opentelemetry.io/concepts/signals/metrics/), and[logs](https://opentelemetry.io/concepts/signals/logs/).**Open source**, as well as**vendor- and tool-agnostic**, meaning that it can be used with a broad variety of observability backends, including open source tools like[Jaeger](https://www.jaegertracing.io/)and[Prometheus](https://prometheus.io/), as well as commercial offerings. OpenTelemetry is**not**an observability backend itself.

A major goal of OpenTelemetry is to enable easy instrumentation of your applications and systems, regardless of the programming language, infrastructure, and runtime environments used.

The backend (storage) and the frontend (visualization) of telemetry data are intentionally left to other tools.

For more videos in this series and additional resources, see
[What next?](https://opentelemetry.io#what-next)

[Observability](https://opentelemetry.io/concepts/observability-primer/#what-is-observability) is the ability to understand the internal state of a system by
examining its outputs.

In software, this is typically achieved by analyzing telemetry data such as traces, metrics, and logs.

To make a system observable, it must be [instrumented](https://opentelemetry.io/concepts/instrumentation). That is, the code
must emit [traces](https://opentelemetry.io/concepts/signals/traces/), [metrics](https://opentelemetry.io/concepts/signals/metrics/), or [logs](https://opentelemetry.io/concepts/signals/logs/). The instrumented data must then
be sent to an observability backend.

With the rise of cloud computing, microservices architectures, and increasingly
complex business requirements, the need for software and infrastructure
[observability](https://opentelemetry.io/concepts/observability-primer/#what-is-observability) is greater than ever.

OpenTelemetry satisfies the need for observability while following two key principles:

- You own the data that you generate. There’s no vendor lock-in.
- You only have to learn a single set of APIs and conventions.

Both principles combined grant teams and organizations the flexibility they need in today’s modern computing world.

If you want to learn more, take a look at OpenTelemetry’s
[mission, vision, and values](https://opentelemetry.io/community/mission/).

OpenTelemetry consists of the following major components:

- A
[specification](https://opentelemetry.io/docs/specs/otel/)for all components - A standard
[protocol](https://opentelemetry.io/docs/specs/otlp/)that defines the shape of telemetry data [Semantic conventions](https://opentelemetry.io/docs/specs/semconv/)that define a standard naming scheme for common telemetry data types- APIs that define how to generate telemetry data
[Language SDKs](https://opentelemetry.io/languages)that implement the specification, APIs, and export of telemetry data- A
[library ecosystem](https://opentelemetry.io/ecosystem/registry/)that implements instrumentation for common libraries and frameworks - Automatic instrumentation components that generate telemetry data without requiring code changes
- The
[OpenTelemetry Collector](https://opentelemetry.io/collector), a proxy that receives, processes, and exports telemetry data - Various other tools, such as the
[OpenTelemetry Operator for Kubernetes](https://opentelemetry.io/platforms/kubernetes/operator/),[OpenTelemetry Helm Charts](https://opentelemetry.io/platforms/kubernetes/helm/), and[community assets for FaaS](https://opentelemetry.io/platforms/faas/)

OpenTelemetry is used by a wide variety of
[libraries, services and apps](https://opentelemetry.io/ecosystem/integrations/) that have OpenTelemetry
integrated to provide observability by default.

OpenTelemetry is supported by numerous [vendors](https://opentelemetry.io/ecosystem/vendors/), many of
whom provide commercial support for OpenTelemetry and contribute to the project
directly.

OpenTelemetry is designed to be extensible. Some examples of how it can be extended include:

- Adding a receiver to the OpenTelemetry Collector to support telemetry data from a custom source
- Loading custom instrumentation libraries into an SDK
- Creating a
[distribution](https://opentelemetry.io/concepts/distributions/)of an SDK or the Collector tailored to a specific use case - Creating a new exporter for a custom backend that doesn’t yet support the OpenTelemetry protocol (OTLP)
- Creating a custom propagator for a nonstandard context propagation format

Although most users might not need to extend OpenTelemetry, the project is designed to make it possible at nearly every level.

OpenTelemetry is a [Cloud Native Computing Foundation](https://www.cncf.io) (CNCF) project that is
the result of a [merger](https://www.cncf.io/blog/2019/05/21/a-brief-history-of-opentelemetry-so-far/) between two prior projects,
[OpenTracing](https://opentracing.io) and [OpenCensus](https://opencensus.io).
Both of these projects were created to solve the same problem: the lack of a
standard for how to instrument code and send telemetry data to an Observability
backend. As neither project was fully able to solve the problem independently,
they merged to form OpenTelemetry and combine their strengths while offering a
single solution.

If you are currently using OpenTracing or OpenCensus, you can learn how to
migrate to OpenTelemetry in the [Migration guide](https://opentelemetry.io/compatibility/migration/).

[Getting started](https://opentelemetry.io/getting-started/)— jump right in!- Learn about
[OpenTelemetry concepts](https://opentelemetry.io/concepts/). [Watch videos](https://www.youtube.com/@otel-official)from the[OTel for beginners](https://www.youtube.com/playlist?list=PLVYDBkQ1TdyyWjeWJSjXYUaJFVhplRtvN)or other[playlists](https://www.youtube.com/@otel-official/playlists).- Sign up for
[training](https://opentelemetry.io/training/), including the**free course**[Getting started with OpenTelemetry](https://opentelemetry.io/training/#courses).

Was this page helpful?

Thank you. Your feedback is appreciated!

Please let us know [how we can improve this page](https://github.com/open-telemetry/opentelemetry.io/issues/new?template=PAGE_FEEDBACK.yml&title=[Page+feedback]%3A+ADD+A+SUMMARY+OF+YOUR+FEEDBACK+HERE). Your feedback is appreciated!
