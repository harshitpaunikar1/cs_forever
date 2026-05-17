Title: Cluster Administration | Kubernetes
Mapped Topic: Kubernetes concepts and tutorials
Source URL: https://kubernetes.io/docs/concepts/cluster-administration/
Source Type: official_docs
Trust Score: 98
Fetched At: 2026-04-17T07:11:15+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

Lower-level detail relevant to creating or administering a Kubernetes cluster.

The cluster administration overview is for anyone creating or administering a Kubernetes cluster.
It assumes some familiarity with core Kubernetes [concepts](https://kubernetes.io/docs/concepts/).

See the guides in [Setup](https://kubernetes.io/docs/setup/) for examples of how to plan, set up, and configure
Kubernetes clusters. The solutions listed in this article are called *distros*.

Before choosing a guide, here are some considerations:

- Do you want to try out Kubernetes on your computer, or do you want to build a high-availability, multi-node cluster? Choose distros best suited for your needs.
- Will you be using
**a hosted Kubernetes cluster**, such as[Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/), or**hosting your own cluster**? - Will your cluster be
**on-premises**, or**in the cloud (IaaS)**? Kubernetes does not directly support hybrid clusters. Instead, you can set up multiple clusters. **If you are configuring Kubernetes on-premises**, consider which[networking model](https://kubernetes.io/docs/concepts/cluster-administration/networking/)fits best.- Will you be running Kubernetes on
**"bare metal" hardware**or on**virtual machines (VMs)**? - Do you
**want to run a cluster**, or do you expect to do**active development of Kubernetes project code**? If the latter, choose an actively-developed distro. Some distros only use binary releases, but offer a greater variety of choices. - Familiarize yourself with the
[components](https://kubernetes.io/docs/concepts/overview/components/)needed to run a cluster.

Learn how to

[manage nodes](https://kubernetes.io/docs/concepts/architecture/nodes/).- Read about
[Node autoscaling](https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/).

- Read about
Learn how to set up and manage the

[resource quota](https://kubernetes.io/docs/concepts/policy/resource-quotas/)for shared clusters.

[Generate Certificates](https://kubernetes.io/docs/tasks/administer-cluster/certificates/)describes the steps to generate certificates using different tool chains.[Kubernetes Container Environment](https://kubernetes.io/docs/concepts/containers/container-environment/)describes the environment for Kubelet managed containers on a Kubernetes node.[Controlling Access to the Kubernetes API](https://kubernetes.io/docs/concepts/security/controlling-access/)describes how Kubernetes implements access control for its own API.[Authenticating](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)explains authentication in Kubernetes, including the various authentication options.[Authorization](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)is separate from authentication, and controls how HTTP calls are handled.[Using Admission Controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)explains plug-ins which intercepts requests to the Kubernetes API server after authentication and authorization.[Admission Webhook Good Practices](https://kubernetes.io/docs/concepts/cluster-administration/admission-webhooks-good-practices/)provides good practices and considerations when designing mutating admission webhooks and validating admission webhooks.[Using Sysctls in a Kubernetes Cluster](https://kubernetes.io/docs/tasks/administer-cluster/sysctl-cluster/)describes to an administrator how to use the`sysctl`

command-line tool to set kernel parameters .[Auditing](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)describes how to interact with Kubernetes' audit logs.

[DNS Integration](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)describes how to resolve a DNS name directly to a Kubernetes service.[Logging and Monitoring Cluster Activity](https://kubernetes.io/docs/concepts/cluster-administration/logging/)explains how logging in Kubernetes works and how to implement it.

Last modified February 03, 2025 at 5:28 PM PST: [Add a new page for mutating webhook good practices. (bf971d28d3)](https://github.com/kubernetes/website/commit/bf971d28d3b485726e8e6b3a502626de5852256f)
