Title: Installing RabbitMQ | RabbitMQ
Mapped Topic: Queues and message-driven systems
Source URL: https://www.rabbitmq.com/docs/download
Source Type: official_docs
Trust Score: 93
Fetched At: 2026-04-17T07:09:14+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Installing RabbitMQ

The latest [release](https://github.com/rabbitmq/rabbitmq-server/releases) of RabbitMQ is **4.2.5**. See [change log](https://www.rabbitmq.com/release-information) for release notes.
See [RabbitMQ support timeline](https://www.rabbitmq.com/release-information) to find out what release series are supported.

Experimenting with RabbitMQ on your workstation? Try the [community Docker image](https://hub.docker.com/_/rabbitmq/):

`# latest RabbitMQ 4.x`

docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4-management

## Open Source RabbitMQ Server[](https://www.rabbitmq.com#open-source-rabbitmq-server)

### Installation Guides[](https://www.rabbitmq.com#installation-guides)

- Linux, BSD, UNIX:
[Debian, Ubuntu](https://www.rabbitmq.com/docs/install-debian)|[RHEL, CentOS Stream, Fedora](https://www.rabbitmq.com/docs/install-rpm)|[Generic binary build](https://www.rabbitmq.com/docs/install-generic-unix)|[Solaris](https://www.rabbitmq.com/docs/install-solaris) - Windows:
[Chocolatey package](https://community.chocolatey.org/packages/rabbitmq)|[Windows Installer](https://www.rabbitmq.com/docs/install-windows)|[Binary build](https://www.rabbitmq.com/docs/install-windows-manual) - MacOS:
[Homebrew](https://www.rabbitmq.com/docs/install-homebrew)|[Generic binary build](https://www.rabbitmq.com/docs/install-generic-unix) [Erlang/OTP for RabbitMQ](https://www.rabbitmq.com/docs/which-erlang)

### Preview Releases[](https://www.rabbitmq.com#preview-releases)

You can contribute to open source RabbitMQ by helping the community test [preview releases](https://github.com/rabbitmq/rabbitmq-server/releases).
They are marked as pre-releases on GitHub.

## VMware Tanzu RabbitMQ (Commercial Editions)[](https://www.rabbitmq.com#vmware-tanzu-rabbitmq-commercial-editions)

[VMware Tanzu RabbitMQ OVA](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-rabbitmq-ova/4-2/tanzu-rabbitmq-ova-virtual-machine/site-overview.html)[VMware Tanzu RabbitMQ RPM](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-rabbitmq-rpm/4-2/tanzu-rabbitmq-rpm-offering/site-overview.html)[VMware Tanzu RabbitMQ OCI](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-rabbitmq-oci/4-2/tanzu-rabbitmq-oci-image/site-overview.html)[VMware Tanzu RabbitMQ on Kubernetes](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-rabbitmq-on-kubernetes/4-2/tanzu-rabbitmq-kubernetes/overview.html)

## Kubernetes[](https://www.rabbitmq.com#kubernetes)

### RabbitMQ Cluster Kubernetes Operator[](https://www.rabbitmq.com#rabbitmq-cluster-kubernetes-operator)

Open source [RabbitMQ Cluster Kubernetes Operator](https://www.rabbitmq.com/kubernetes/operator/operator-overview) by VMware (developed [on GitHub](https://github.com/rabbitmq/cluster-operator)):

### RabbitMQ Topology Kubernetes Operator[](https://www.rabbitmq.com#rabbitmq-topology-kubernetes-operator)

Open source [RabbitMQ Topology Kubernetes Operator](https://www.rabbitmq.com/kubernetes/operator/using-topology-operator) by VMware (developed [on GitHub](https://github.com/rabbitmq/messaging-topology-operator)):

Other guides related to Kubernetes:

- A
[peer discovery](https://www.rabbitmq.com/docs/cluster-formation)mechanism[for Kubernetes](https://www.rabbitmq.com/docs/cluster-formation#peer-discovery-k8s)

## Docker[](https://www.rabbitmq.com#docker)

- Docker community-maintained
[RabbitMQ Docker image](https://hub.docker.com/_/rabbitmq/)([on GitHub](https://github.com/docker-library/rabbitmq/))

## Cloud[](https://www.rabbitmq.com#cloud)

[VMware Tanzu RabbitMQ®](https://tanzu.vmware.com/rabbitmq)[RabbitMQ Cluster Kubernetes Operator](https://www.rabbitmq.com/kubernetes/operator/install-operator)by VMware (developed[on GitHub](https://github.com/rabbitmq/cluster-operator))[VMware Tanzu RabbitMQ® on Kubernetes](https://docs.vmware.com/en/VMware-Tanzu-RabbitMQ-for-Kubernetes/3.13/tanzu-rabbitmq-kubernetes/installation.html)[Amazon MQ for RabbitMQ](https://aws.amazon.com/amazon-mq/)[Amazon EC2](https://www.rabbitmq.com/docs/ec2)

## Downloads [on GitHub](https://github.com/rabbitmq/rabbitmq-server/releases)[](https://www.rabbitmq.com#downloads-on-github)

-
[Windows Installer](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-4.2.5.exe) -
[Debian, Ubuntu](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server_4.2.5-1_all.deb) [RHEL, CentOS Stream 9.x, CentOS 8.x](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-4.2.5-1.el8.noarch.rpm)| zero dependency[Erlang RPM](https://github.com/rabbitmq/erlang-rpm)-
[Generic UNIX binary](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-generic-unix-4.2.5.tar.xz) -
[Windows binary](https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-windows-4.2.5.zip)

## Debian (Apt) and RPM (Yum) Repositories[](https://www.rabbitmq.com#debian-apt-and-rpm-yum-repositories)

## Provisioning Tools (Chef, Puppet, etc)[](https://www.rabbitmq.com#provisioning-tools-chef-puppet-etc)

## Release Signing Key[](https://www.rabbitmq.com#release-signing-key)

[Release Signing Key](https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc)`0x6B73A36E6026DFCA`

(on GitHub)[How to Verify Release Artifact Signatures](https://www.rabbitmq.com/docs/signatures)[Release Signing Key](https://www.rabbitmq.com/assets/files/rabbitmq-release-signing-key-24901c1305e0b467719d263a6b736713.asc)(alternative download location on rabbitmq.com)

## Client Libraries[](https://www.rabbitmq.com#client-libraries)

### Java Client[](https://www.rabbitmq.com#java-client)

- On Maven Central:
[RabbitMQ Java client](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.rabbitmq%22%20AND%20a%3A%22amqp-client%22) - Quick download:
[Maven.org](https://repo1.maven.org/maven2/com/rabbitmq/amqp-client/5.30.0/amqp-client-5.30.0.jar) [API guide](https://www.rabbitmq.com/client-libraries/java-api-guide)[API reference](https://rabbitmq.github.io/rabbitmq-java-client/api/current/)(JavaDoc)[License and other information](https://www.rabbitmq.com/client-libraries/java-client)[Older versions](https://repo1.maven.org/maven2/com/rabbitmq/amqp-client/)

### Java [Stream Protocol](https://www.rabbitmq.com/docs/streams) Client[](https://www.rabbitmq.com#java-stream-protocol-client)

### JMS Client[](https://www.rabbitmq.com#jms-client)

- On Maven Central:
[RabbitMQ JMS Client](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.rabbitmq.jms%22%20AND%20a%3A%22rabbitmq-jms%22)

### .NET/C# Client[](https://www.rabbitmq.com#netc-client)

### .NET/C# [Stream Protocol](https://www.rabbitmq.com/docs/streams) Client[](https://www.rabbitmq.com#netc-stream-protocol-client)

### Erlang Client[](https://www.rabbitmq.com#erlang-client)

- On Hex.pm:
[amqp_client](https://hex.pm/packages/amqp_client)

### Clients for Other Languages[](https://www.rabbitmq.com#clients-for-other-languages)

The RabbitMQ community has created a large number of [clients and developer tools](https://www.rabbitmq.com/client-libraries/devtools)
covering a variety of platforms and languages.

## Community Plugins[](https://www.rabbitmq.com#community-plugins)

For your convenience, we offer binary downloads of various plugins developed by the community.

## Snapshot (Alpha) Builds[](https://www.rabbitmq.com#snapshot-alpha-builds)

Snapshot releases of the RabbitMQ broker
available to users who wish to experiment with the latest and
greatest features and bug fixes. For more details, head over to
the [snapshots page](https://www.rabbitmq.com/docs/snapshots).
