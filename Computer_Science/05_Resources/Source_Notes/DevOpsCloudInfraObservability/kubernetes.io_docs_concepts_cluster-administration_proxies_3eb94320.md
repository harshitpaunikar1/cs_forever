Title: Proxies in Kubernetes | Kubernetes
Mapped Topic: Kubernetes concepts and tutorials
Source URL: https://kubernetes.io/docs/concepts/cluster-administration/proxies/
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:11:44+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

This page explains proxies used with Kubernetes.

There are several different proxies you may encounter when using Kubernetes:

The

[kubectl proxy](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/#directly-accessing-the-rest-api):- runs on a user's desktop or in a pod
- proxies from a localhost address to the Kubernetes apiserver
- client to proxy uses HTTP
- proxy to apiserver uses HTTPS
- locates apiserver
- adds authentication headers

The

[apiserver proxy](https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster-services/#discovering-builtin-services):- is a bastion built into the apiserver
- connects a user outside of the cluster to cluster IPs which otherwise might not be reachable
- runs in the apiserver processes
- client to proxy uses HTTPS (or http if apiserver so configured)
- proxy to target may use HTTP or HTTPS as chosen by proxy using available information
- can be used to reach a Node, Pod, or Service
- does load balancing when used to reach a Service

The

[kube proxy](https://kubernetes.io/docs/concepts/services-networking/service/#ips-and-vips):- runs on each node
- proxies UDP, TCP and SCTP
- does not understand HTTP
- provides load balancing
- is only used to reach services

A Proxy/Load-balancer in front of apiserver(s):

- existence and implementation varies from cluster to cluster (e.g. nginx)
- sits between all clients and one or more apiservers
- acts as load balancer if there are several apiservers.

Cloud Load Balancers on external services:

- are provided by some cloud providers (e.g. AWS ELB, Google Cloud Load Balancer)
- are created automatically when the Kubernetes service has type
`LoadBalancer`

- usually supports UDP/TCP only
- SCTP support is up to the load balancer implementation of the cloud provider
- implementation varies by cloud provider.

Kubernetes users will typically not need to worry about anything other than the first two types. The cluster admin will typically ensure that the latter types are set up correctly.

Proxies have replaced redirect capabilities. Redirects have been deprecated.

Last modified October 24, 2022 at 1:43 PM PST: [KubeCon Docs Sprint: Update page weights for content/en/docs/concepts/cluster-administration. (ac5e7c0bd0)](https://github.com/kubernetes/website/commit/ac5e7c0bd046d4ba88c1cf5f9a624e8fbe4d9193)
