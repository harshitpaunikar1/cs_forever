Title: Coordinated Leader Election | Kubernetes
Mapped Topic: Kubernetes concepts and tutorials
Source URL: https://kubernetes.io/docs/concepts/cluster-administration/coordinated-leader-election/
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:11:27+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

FEATURE STATE:

`Kubernetes v1.33 [beta]`

(disabled by default)Kubernetes 1.35 includes a beta feature that allows [control plane](https://kubernetes.io/docs/reference/glossary/?all=true#term-control-plane) components to
deterministically select a leader via *coordinated leader election*.
This is useful to satisfy Kubernetes version skew constraints during cluster upgrades.
Currently, the only builtin selection strategy is `OldestEmulationVersion`

,
preferring the leader with the lowest emulation version, followed by binary
version, followed by creation timestamp.

Ensure that `CoordinatedLeaderElection`

[feature
gate](https://kubernetes.io/docs/reference/command-line-tools-reference/feature-gates/) is enabled
when you start the [API Server](https://kubernetes.io/docs/concepts/architecture/#kube-apiserver): and that the `coordination.k8s.io/v1beta1`

API group is
enabled.

This can be done by setting flags `--feature-gates="CoordinatedLeaderElection=true"`

and
`--runtime-config="coordination.k8s.io/v1beta1=true"`

.

Provided that you have enabled the `CoordinatedLeaderElection`

feature gate *and*

have the `coordination.k8s.io/v1beta1`

API group enabled, compatible control plane

components automatically use the LeaseCandidate and Lease APIs to elect a leader

as needed.

For Kubernetes 1.35, two control plane components

(kube-controller-manager and kube-scheduler) automatically use coordinated

leader election when the feature gate and API group are enabled.

Kubernetes uses the [Lease API](https://kubernetes.io/docs/concepts/architecture/leases/) to perform leader election among multiple instances of the same control-plane component in a high-availability cluster, such as `kube-controller-manager`

or `kube-scheduler`

.

A [Lease](https://kubernetes.io/docs/concepts/architecture/leases/) acts as a lightweight distributed lock. stored by the [Kubernetes API server](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/).
All running instances of a component watch or periodically read the relevant Lease object
to determine which instance is currently acting as the leader.

The [Lease API](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/lease-v1/) defines fields
such as:

`holderIdentity`

- the identity (for example: pod name or hostname-based string) of the current leader.
`acquireTime`

- timestamp when leadership was acquired.
`renewTime`

- timestamp of the most recent renewal by the leader.
`leaseDurationSeconds`

- the validity period of the lease (candidates should wait this long plus a small grace period before attempting to acquire an expired lease).
`leaseTransitions`

- counter of how many times leadership has changed hands.

These fields indicate which instance holds leadership and how long that leadership remains valid.

When the [Lease](https://kubernetes.io/docs/concepts/architecture/leases/) does not exist or has expired (current time > `renewTime`

+ `leaseDurationSeconds`

), candidate instances attempt to update the Lease with their identity. Kubernetes relies on *optimistic concurrency control* via the object's `resourceVersion`

: only one update succeeds due to version mismatch on concurrent attempts. The instance whose update is accepted becomes the *leader*.

Kubernetes uses the [LeaseCandidate](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/lease-candidate-v1beta1/)
API to manage leader elections. Control plane components such as `kube-controller-manager`

and `kube-scheduler`

register their role as a candidate by creating LeaseCandidate objects, which track all instances competing for leadership and carry metadata including the candidate's identity, binary version, and emulation version.

During an election, candidates coordinate through a shared [Lease](https://kubernetes.io/docs/concepts/architecture/leases/).
The Kubernetes control plane guarantees that only one candidate successfully acquires the [Lease](https://kubernetes.io/docs/concepts/architecture/leases/) and assumes the role of *leader*, while all others remain as followers. If the current *leader* fails to renew the [Lease](https://kubernetes.io/docs/concepts/architecture/leases/) within the selected timeout period, the remaining candidates compete to acquire leadership and elect a new *leader*.

Once elected, the leader periodically renews its Lease by updating the `renewTime`

field

(for example, performing renewal every `leaseDurationSeconds`

÷ 2, in order to avoid conflicts when the [Lease](https://kubernetes.io/docs/concepts/architecture/leases/) is about to expire).
As long as renewals occur before the lease expires, the current leader instance retains leadership.
If the leader crashes, becomes unreachable, or stops renewing the Lease, that Lease expires. Other healthy instances detect the expired Lease and attempt a new election.

This mechanism ensures that even though multiple replicas of a component may be running for stability and recovery, *only one instance actively performs control tasks at a time*, while the others remain on standby, watching the Lease and ready to take over quickly if needed.

Last modified March 09, 2026 at 6:43 PM PST: [Lease API (7d0638aae7)](https://github.com/kubernetes/website/commit/7d0638aae73425ce7d12dabf5b5867b1f30819fa)
