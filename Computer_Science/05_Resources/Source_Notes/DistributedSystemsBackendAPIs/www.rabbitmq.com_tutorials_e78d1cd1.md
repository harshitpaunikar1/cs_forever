Title: RabbitMQ Tutorials | RabbitMQ
Mapped Topic: Queues and message-driven systems
Source URL: https://www.rabbitmq.com/tutorials
Source Type: official_docs
Trust Score: 93
Fetched At: 2026-04-17T07:09:11+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# RabbitMQ Tutorials

These tutorials cover the basics of creating messaging applications using RabbitMQ.

You need to have the RabbitMQ server installed to go through the tutorials,
please see the [installation guide](https://www.rabbitmq.com/docs/download) or use the [community Docker image](https://hub.docker.com/_/rabbitmq/).

Executable versions of these tutorials [are open source](https://github.com/rabbitmq/rabbitmq-tutorials),
as is [this website](https://github.com/rabbitmq/rabbitmq-website).

There are two groups of tutorials:

This tutorials target RabbitMQ 4.x.

### Queue tutorials[](https://www.rabbitmq.com#queue-tutorials)

This section covers the default RabbitMQ protocol, AMQP 0-9-1.

## 1. "Hello World!" | ## 2. Work Queues | ## 3. Publish/Subscribe |
## 4. Routing | ## 5. Topics | ## 6. RPC |
## 7. Publisher Confirms |

## AMQP 0-9-1 Overview[](https://www.rabbitmq.com#amqp-0-9-1-overview)

Once you have been through the tutorials (or if you want to
skip ahead), you may wish to read an
[Introduction to RabbitMQ Concepts](https://www.rabbitmq.com/tutorials/amqp-concepts)
and take a look at the [Compatibility and Conformance page](https://www.rabbitmq.com/docs/specification)
to find relevant resources to learn more about AMQP 1.0 and AMQP 0-9-1,
the two core protocols implemented by RabbitMQ.

## Stream tutorials[](https://www.rabbitmq.com#stream-tutorials)

This section covers [RabbitMQ streams](https://www.rabbitmq.com/docs/streams).

## 1. "Hello World!" | ## 2. Offset Tracking |

## Stream Overview and Blog Posts[](https://www.rabbitmq.com#stream-overview-and-blog-posts)

Once you have been through the tutorials (or if you want to
skip ahead), you may wish to read the
[RabbitMQ stream documentation](https://www.rabbitmq.com/docs/streams)
and browse our
[stream blog posts](https://www.rabbitmq.com/blog/tags/streams).

## Getting Help[](https://www.rabbitmq.com#getting-help)

If you have any questions or comments regarding RabbitMQ, feel free to
ask them on [GitHub Discussion](https://github.com/rabbitmq/rabbitmq-server/discussions) or
[RabbitMQ community Discord server](https://www.rabbitmq.com/discord).

## Tutorials in Other Languages[](https://www.rabbitmq.com#tutorials-in-other-languages)

The tutorials here use a number of popular technologies,
however, there are [ports available](https://github.com/rabbitmq/rabbitmq-tutorials) for
many more languages and client libraries, for example:

- Rust using
[amqprs](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/rust-amqprs) - Rust using
[Lapin](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/rust-lapin) [Clojure](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/clojure)(using[Langohr](http://clojurerabbitmq.info))[Erlang](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/erlang)(using[RabbitMQ Erlang client](https://github.com/rabbitmq/rabbitmq-erlang-client))[Haskell](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/haskell)(using[Network.AMQP](http://hackage.haskell.org/package/amqp))[Perl](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/perl)(using[Net::RabbitFoot](https://github.com/cooldaemon/RabbitFoot))[Perl](https://github.com/oylenshpeegul/RabbitMQ-Tutorial-Perl)(using[Net::AMQP::RabbitMQ](http://p3rl.org/Net::AMQP::RabbitMQ))[Scala](https://github.com/rabbitmq/rabbitmq-tutorials/tree/main/scala)(using[RabbitMQ Java client](https://www.rabbitmq.com/client-libraries/java-api-guide))

We also maintain a list of community-developed [clients and developer tools](https://www.rabbitmq.com/client-libraries/devtools)
for various protocols RabbitMQ supports.
