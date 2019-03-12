@transition[none]

@size[40pt](@color[#FF694B](**Kubernetes Under the Hood**)@color[#333F48](: <br />A deep dive into container runtimes))

@snap[south]
@size[18pt](Jake Remitz | Lead Software DevOps Engineer) <br />
@size[14pt](@fa[github] @fa[twitter-square] @jremitz)
@snapend

---
@transition[none]
@snap[north text-bold text-capitalize h1 span-100]
OVERVIEW
@snapend


@snap[midpoint span-500 text-08]
Container runtimes are behind the scenes, this is a high level, surface look at those runtimes.
@snapend
@snap[midpoint span-200]
@ol[text-07](false)
- Presentation goals
- Introduction to "containers"
    a. Open Container Initiative ("OCI")
    a. Runtime spec vs. Image spec
- Introduction to Kubernetes
    a. Architecture
    a. Container Runtime Interface ("CRI")
- Kubernetes' Container Runtimes
- Introduction to Micro VMs
- Installing Kubernetes
- Demonstration
@olend
@snapend
---

### Goals

- Desire to understand Kubernetes' dependencies
- Many underlying technologies that have their own feature sets often not seen or considered
- Awareness to new stakeholders including: architecture, security, and operations (among others)

---
### Container Overview

> Linux containers are implementations of operating system-level virtualization for the Linux operating system. Several implementations exist, all based on the virtualization, isolation, and resource management mechanisms provided by the Linux kernel, notably Linux namespaces and cgroups.

[Wikipedia.org](https://en.wikipedia.org/wiki/List_of_Linux_containers)

+++

### Containers: LXC versus Docker

![LXC versus Docker from Stack Exchange](https://i.stack.imgur.com/a5Neb.png)

@css[text-06]([Stack Exchange](https://unix.stackexchange.com/a/254982))

+++

#### Open Container Initiative ("OCI")

- Started by Docker, CoreOS, and others in 2015
- Attempt to standardize runtimes and image specs for community development
    - @size[14pt]([Runtime Spec](https://github.com/opencontainers/runtime-spec))
    - @size[14pt]([Image Spec](https://github.com/opencontainers/image-spec))
- Runtime CLI for OCI spec - ["runc"](https://github.com/opencontainers/runc)
    - Versions of runc are tightly coupled with versions of OCI runtime-spec

+++ 
#### OCI Compliant Runtimes

- runc - opencontainer runtime
- runv - hypervisor-based runtime
- runhcs - Windows container host counterpart to runc
- runsc - gVisor runtime by Google
- virtcontainers - hypervisor-based runtime for kata-containers
- cc-runtime (deprecated) - hypervisor-based runtime

---
### Kubernetes: what is it?

> Kubernetes (K8s) is an open-source system for automating deployment, scaling, and management of containerized applications.
> 
> It groups containers that make up an application into logical units for easy management and discovery.

[kubernetes.io](https://kubernetes.io/)

+++
#### Kubernetes Architectural Overview

![Kubernetes Components](https://d33wubrfki0l68.cloudfront.net/e298a92e2454520dddefc3b4df28ad68f9b91c6f/70d52/images/docs/pre-ccm-arch.png)

+++
@transition[none]
@snap[north text-bold text-capitalize h1 span-100]
<br />
CONTAINER RUNTIME INTERFACE (CRI)
@snapend

@snap[west span-40]
@ul[text-06](false)
- Introduced in kubernetes 1.5
- Container Runtimes (Docker/Rkt) had been embedded in k8s
- Incorporated into the Kubelet which runs on the Node
- Leverages gRPC calls for common functions like stopping/starting containers, and other things
@ulend
@snapend

@snap[east sidebar span-55]
![CRI Overview](/src/img/cri_overview.png)
@snapend

---
@transition[none]
@snap[north text-bold text-capitalize h1 span-100]
<br />
KUBERNETES CONTAINER RUNTIMES
@snapend

@snap[midpoint span-100]
@ul[text-06](false)
- Docker
- Containerd
- CRI-O
- Frakti
- Rkt (inactive)
@ulend
@snapend

+++
#### Docker

- Default container runtime for most installations
- References dockershim which is built into Kubelet
- leverages `runc` as OCI runtime

![CRI Docker](/src/img/cri-docker.png)

+++
#### Containerd

- Has built in API for handling CRI calls
- Supports multiple OCI runtimes
- Default runtime is `runc`, can handle untrusted/trusted workloads
- Support Kubernetes RuntimeClasses (alpha w/ v1.12)
- Support kata-containers

![CRI Containerd](/src/img/cri-containerd.png)

+++
#### CRI-O

- Default with Openshift installation
- Built specifically for Kubernetes
- Supports multiple OCI runtimes
- Default runtime is `runc`, can handle untrusted/trusted workloads
- Support Kubernetes RuntimeClasses (alpha w/ v1.12)
- Support kata-containers

![CRI CRI-O](/src/img/cri-crio.png)

+++

#### Frakti

- Default runtime is `runv`
- Runs pods in hypervisors via runv/hyperd
- Supports multiple OCI runtimes, for use with Docker as well

![CRI Frakti](/src/img/cri-frakti.png)

---

### Kata-containers

- Based on Intel's Clear Containers with help from Openstack Foundation
- Requires nested virtualization on the VM (e.g. AWS' i3.metal)
- Runtime of `virtcontainers`
- Runs qemu-lite virtual machines
- Supports AWS' Firecracker-based virtual machines (January, 2019)
- Supports IBM Z-series (s390x) (January, 2019)

---

### Kubernetes Installation Methods

Limitations exist for CRI support:
- EKS (AWS)
- GKE (Google Cloud)
- IBM Cloud Kubernetes
- Kops
- KubeSpray
- @color[#FF694B](Kubeadm)
- Kubic
- PKS
- _..._

---

### Demonstration

@css[text-bold](Frankenstein's Kubernetes)

@img[span-30](http://hddfhm.com/images/clipart-frankenstein-18.png)

+++

#### K8s Architecture

![Frankenstein's K8s Architecture](/src/img/frankensteins-k8s.png)

---
@transition[none]
@snap[north text-bold text-capitalize h1 span-100]
<br />
SUMMARY
@snapend

@snap[west span-200]
@ul[text-06](false)
- Container runtimes and options may be different based on k8s installation method
- Container runtime development is happening in parallel to Kubernetes development, not just downstream
- Kubernetes requirements can extend beyond customer experience (e.g. security), raising needs for broader decisions on runtime configuration
- Kubernetes features can be tied to container runtime capabilities
@ulend
@snapend

---
### Glossary

- CNI - [Container Network Interface](https://github.com/containernetworking/cni#cni---the-container-network-interface) - network connectivity of containers
- CRI - Container Runtime Interface - K8s 1.5+ - Of the lowest layers of a Kubernetes node is the software that, among other things, starts and stops containers
- CSI - Container Storage Interface - K8s 1.9+ - standardized mechanism for Container Orchestration Systems (COs) to expose arbitrary storage systems to their containerized workloads
- [Pod Sandbox](https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/) - A Pod is composed of a group of application containers in an isolated environment with resource constraints

