Title: Cloud Controller Manager | Kubernetes
Mapped Topic: Kubernetes concepts and tutorials
Source URL: https://kubernetes.io/docs/concepts/architecture/cloud-controller/
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:10:56+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

FEATURE STATE:

`Kubernetes v1.11 [beta]`

Cloud infrastructure technologies let you run Kubernetes on public, private, and hybrid clouds. Kubernetes believes in automated, API-driven infrastructure without tight coupling between components.

The cloud-controller-manager is a Kubernetes [control plane](https://kubernetes.io/docs/reference/glossary/?all=true#term-control-plane) component
that embeds cloud-specific control logic. The cloud controller manager lets you link your
cluster into your cloud provider's API, and separates out the components that interact
with that cloud platform from components that only interact with your cluster.

By decoupling the interoperability logic between Kubernetes and the underlying cloud infrastructure, the cloud-controller-manager component enables cloud providers to release features at a different pace compared to the main Kubernetes project.

The cloud-controller-manager is structured using a plugin mechanism that allows different cloud providers to integrate their platforms with Kubernetes.

The cloud controller manager runs in the control plane as a replicated set of processes
(usually, these are containers in Pods). Each cloud-controller-manager implements
multiple [controllers](https://kubernetes.io/docs/concepts/architecture/controller/) in a single
process.

The controllers inside the cloud controller manager include:

The node controller is responsible for updating [Node](https://kubernetes.io/docs/concepts/architecture/nodes/) objects
when new servers are created in your cloud infrastructure. The node controller obtains information about the
hosts running inside your tenancy with the cloud provider. The node controller performs the following functions:

- Update a Node object with the corresponding server's unique identifier obtained from the cloud provider API.
- Annotating and labelling the Node object with cloud-specific information, such as the region the node is deployed into and the resources (CPU, memory, etc) that it has available.
- Obtain the node's hostname and network addresses.
- Verifying the node's health. In case a node becomes unresponsive, this controller checks with your cloud provider's API to see if the server has been deactivated / deleted / terminated. If the node has been deleted from the cloud, the controller deletes the Node object from your Kubernetes cluster.

Some cloud provider implementations split this into a node controller and a separate node lifecycle controller.

The route controller is responsible for configuring routes in the cloud appropriately so that containers on different nodes in your Kubernetes cluster can communicate with each other.

Depending on the cloud provider, the route controller might also allocate blocks of IP addresses for the Pod network.

[Services](https://kubernetes.io/docs/concepts/services-networking/service/) integrate with cloud
infrastructure components such as managed load balancers, IP addresses, network
packet filtering, and target health checking. The service controller interacts with your
cloud provider's APIs to set up load balancers and other infrastructure components
when you declare a Service resource that requires them.

This section breaks down the access that the cloud controller manager requires on various API objects, in order to perform its operations.

The Node controller only works with Node objects. It requires full access to read and modify Node objects.

`v1/Node`

:

- get
- list
- create
- update
- patch
- watch
- delete

The route controller listens to Node object creation and configures routes appropriately. It requires Get access to Node objects.

`v1/Node`

:

- get

The service controller watches for Service object **create**, **update** and **delete** events and then
configures load balancers for those Services appropriately.

To access Services, it requires **list**, and **watch** access. To update Services, it requires
**patch** and **update** access to the `status`

subresource.

`v1/Service`

:

- list
- get
- watch
- patch
- update

The implementation of the core of the cloud controller manager requires access to create Event objects, and to ensure secure operation, it requires access to create ServiceAccounts.

`v1/Event`

:

- create
- patch
- update

`v1/ServiceAccount`

:

- create

The [RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) ClusterRole for the cloud
controller manager looks like:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
name: cloud-controller-manager
rules:
- apiGroups:
- ""
resources:
- events
verbs:
- create
- patch
- update
- apiGroups:
- ""
resources:
- nodes
verbs:
- '*'
- apiGroups:
- ""
resources:
- nodes/status
verbs:
- patch
- apiGroups:
- ""
resources:
- services
verbs:
- list
- watch
- apiGroups:
- ""
resources:
- services/status
verbs:
- patch
- update
- apiGroups:
- ""
resources:
- serviceaccounts
verbs:
- create
- apiGroups:
- ""
resources:
- persistentvolumes
verbs:
- get
- list
- update
- watch
```

[Cloud Controller Manager Administration](https://kubernetes.io/docs/tasks/administer-cluster/running-cloud-controller/#cloud-controller-manager)has instructions on running and managing the cloud controller manager.To upgrade a HA control plane to use the cloud controller manager, see

[Migrate Replicated Control Plane To Use Cloud Controller Manager](https://kubernetes.io/docs/tasks/administer-cluster/controller-manager-leader-migration/).Want to know how to implement your own cloud controller manager, or extend an existing project?

- The cloud controller manager uses Go interfaces, specifically,
`CloudProvider`

interface defined infrom`cloud.go`

[kubernetes/cloud-provider](https://github.com/kubernetes/cloud-provider)to allow implementations from any cloud to be plugged in. - The implementation of the shared controllers highlighted in this document (Node, Route, and Service),
and some scaffolding along with the shared cloudprovider interface, is part of the Kubernetes core.
Implementations specific to cloud providers are outside the core of Kubernetes and implement
the
`CloudProvider`

interface. - For more information about developing plugins,
see
[Developing Cloud Controller Manager](https://kubernetes.io/docs/tasks/administer-cluster/developing-cloud-controller-manager/).

- The cloud controller manager uses Go interfaces, specifically,

Last modified February 11, 2025 at 4:40 PM PST: [Fix some confused cloud-controller documentation (153543263c)](https://github.com/kubernetes/website/commit/153543263ca1ed7c99311e5470665a83ecef82fc)
