Title: Kubernetes Self-Healing | Kubernetes
Mapped Topic: Kubernetes concepts and tutorials
Source URL: https://kubernetes.io/docs/concepts/architecture/self-healing/
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:11:12+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

Kubernetes is designed with self-healing capabilities that help maintain the health and availability of workloads. It automatically replaces failed containers, reschedules workloads when nodes become unavailable, and ensures that the desired state of the system is maintained.

**Container-level restarts:**If a container inside a Pod fails, Kubernetes restarts it based on the.`restartPolicy`

**Replica replacement:**If a Pod in a[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)or[StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)fails, Kubernetes creates a replacement Pod to maintain the specified number of replicas. If a Pod that is part of a[DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)fails, the control plane creates a replacement Pod to run on the same node.**Persistent storage recovery:**If a node is running a Pod with a PersistentVolume (PV) attached, and the node fails, Kubernetes can reattach the volume to a new Pod on a different node.**Load balancing for Services:**If a Pod behind a[Service](https://kubernetes.io/docs/concepts/services-networking/service/)fails, Kubernetes automatically removes it from the Service's endpoints to route traffic only to healthy Pods.

Here are some of the key components that provide Kubernetes self-healing:

Ensures that containers are running, and restarts those that fail.[kubelet](https://kubernetes.io/docs/concepts/architecture/#kubelet):**Deployment (via ReplicaSet), ReplicaSet, StatefulSet and DaemonSet controllers:**Maintain the desired number of Pod replicas.**PersistentVolume controller:**Manages volume attachment and detachment for stateful workloads.

**Storage Failures:**If a persistent volume becomes unavailable, recovery steps may be required.**Application Errors:**Kubernetes can restart containers, but underlying application issues must be addressed separately.

- Read more about
[Pods](https://kubernetes.io/docs/concepts/workloads/pods/) - Learn about
[Kubernetes Controllers](https://kubernetes.io/docs/concepts/architecture/controller/) - Explore
[PersistentVolumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) - Read about
[node autoscaling](https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/). Node autoscaling also provides automatic healing if or when nodes fail in your cluster.

Last modified November 20, 2025 at 8:48 PM PST: [Fix formatting (ac13c80817)](https://github.com/kubernetes/website/commit/ac13c80817b5ca6f21c15e3d686060aaadbec757)
