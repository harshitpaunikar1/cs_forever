Title: APIs | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/apis/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:46+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# APIs

An overview of Redis APIs for developers and operators

Redis provides a number of APIs for developers and operators. The following sections provide you easy access to the client API, the several programmability APIs, the RESTFul management APIs and the Kubernetes resource definitions.

##
APIs for Developers
[
](https://redis.io#apis-for-developers)

###
Client API
[
](https://redis.io#client-api)

Redis comes with a wide range of commands that help you to develop real-time applications. You can find a complete overview of the Redis commands here:

As a developer, you will likely use one of our supported client libraries for connecting and executing commands.

###
Programmability APIs
[
](https://redis.io#programmability-apis)

The existing Redis commands cover most use cases, but if low latency is a critical requirement, you might need to extend Redis' server-side functionality.

Lua scripts have been available since early versions of Redis. With Lua, the script is provided by the client and cached on the server side, which implies the risk that different clients might use a different script version.

The Redis functions feature, which became available in Redis 7, supersedes the use of Lua in prior versions of Redis. The client is still responsible for invoking the execution, but unlike the previous Lua scripts, functions can now be replicated and persisted.

If none of the previous methods fulfills your needs, then you can extend the functionality of Redis with new commands using the Redis Modules API.

##
APIs for Operators
[
](https://redis.io#apis-for-operators)

###
Redis Cloud API
[
](https://redis.io#redis-cloud-api)

Redis Cloud is a fully managed Database as a Service offering and the fastest way to deploy Redis at scale. You can programmatically manage your databases, accounts, access, and credentials using the Redis Cloud REST API.

###
Redis Software API
[
](https://redis.io#redis-software-api)

If you have installed Redis Software, you can automate operations with the Redis Software REST API.

[Redis Software REST API introduction](https://redis.io/docs/latest/operate/rs/references/rest-api/)[Redis Software REST API requests](https://redis.io/docs/latest/operate/rs/references/rest-api/requests/)[Redis Software REST API objects](https://redis.io/docs/latest/operate/rs/references/rest-api/objects/)

###
Redis Enterprise for Kubernetes API
[
](https://redis.io#redis-enterprise-for-kubernetes-api)

If you need to install Redis Enterprise on Kubernetes, then you can use the [Redis Enterprise for Kubernetes Operators](https://redis.io/docs/latest/operate/kubernetes/). You can find the resource definitions here:
