Title: Distributions | OpenTelemetry
Mapped Topic: Traces, metrics, logs, instrumentation
Source URL: https://opentelemetry.io/docs/collector/distributions/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:12:09+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

# Distributions

The OpenTelemetry project currently offers pre-built [distributions](https://github.com/open-telemetry/opentelemetry-collector-releases/tree/main/distributions) of the
Collector. The components included in the distributions can be found by in the
`manifest.yaml`

of each distribution.

## Custom Distributions

Existing distributions provided by the OpenTelemetry project may not meet your
needs. For example, you may want a smaller binary or need to implement custom
functionality like
[authenticator extensions](https://opentelemetry.io/docs/collector/extend/custom-component/extension/authenticator/),
[receivers](https://opentelemetry.io/docs/collector/extend/custom-component/receiver/), processors,
exporters or [connectors](https://opentelemetry.io/docs/collector/extend/custom-component/connector/).
The tool used to build distributions [ocb](https://opentelemetry.io/docs/collector/extend/ocb/)
(OpenTelemetry Collector Builder) is available to build your own distributions.

## Third-party Distributions

Some organizations provide a Collector distribution with additional capabilities or for improved ease of use. What follows is a list of Collector distributions maintained by third parties.

OpenTelemetry **does not validate or endorse** the third-party distributions
listed below. This list is provided as a convenience for the community.

## Adding your Collector distribution

To have your Collector distribution listed, [submit a PR](https://opentelemetry.io/docs/contributing/pull-requests/) with an entry added
to the [distributions list](https://github.com/open-telemetry/opentelemetry.io/tree/main/data/ecosystem/distributions.yaml). The entry should include the following:

- Link to the main page of your distribution
- Link to the documentation that explains how to use the distribution
- GitHub handle or email address as a point of contact so that we can reach out in case we have questions

## Feedback

Was this page helpful?

Thank you. Your feedback is appreciated!

Please let us know [how we can improve this page](https://github.com/open-telemetry/opentelemetry.io/issues/new?template=PAGE_FEEDBACK.yml&title=[Page+feedback]%3A+ADD+A+SUMMARY+OF+YOUR+FEEDBACK+HERE). Your feedback is appreciated!
