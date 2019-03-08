@size[40pt](@color[#FF694B](**Kubernetes Under the Hood**)@color[#333F48](: <br />A deep dive into container runtimes))

@snap[south]
@size[18pt](Jake Remitz | Lead Software DevOps Engineer) <br />
@size[14pt](@fa[github] @fa[twitter-square] @jremitz)
@snapend

Note:

- Jake Remitz - Lead Software DevOps Engineer
- Talk about testing you infrastructure as code (Ansible) in an Enterprise environment
    - reusable, scalable code

---
#### Foreword

@size[16pt](Many technical/owner changes in opensource... interesting journey to identify information)

![Baseketball Map of Sports Team Changes](/src/img/baseketball-map.png)

[Relocation of Professional Sports Teams](https://en.wikipedia.org/wiki/Relocation_of_professional_sports_teams)

---

### Why?

- Lots of talks on Kubernetes and uses, little about how it works
- Many features within Kubernetes to learn and understand for operations, security, and architecture
- Grow awareness and begin focused discussions for community input/feedback

---
### Container Overview

> Linux containers are implementations of operating system-level virtualization for the Linux operating system. Several implementations exist, all based on the virtualization, isolation, and resource management mechanisms provided by the Linux kernel, notably Linux namespaces and cgroups.

[Wikipedia.org](https://en.wikipedia.org/wiki/List_of_Linux_containers)

+++

### LXC versus Docker

![LXC versus Docker from Stack Exchange](https://i.stack.imgur.com/a5Neb.png)

[Stack Exchange Inquiry](https://unix.stackexchange.com/a/254982)

+++

### Open Container Initiative ("OCI")

- Started by Docker, CoreOS, and others in 2015
- Attempt to standardize runtimes and image specs for community development
    - @size[14pt]([Runtime Spec](https://github.com/opencontainers/runtime-spec))
    - @size[14pt]([Image Spec](https://github.com/opencontainers/image-spec))
- Runtime CLI for OCI spec - ["runc"](https://github.com/opencontainers/runc)
    - Versions of runc are tightly coupled with versions of OCI runtime-spec

+++ 
OCI Compliant Runtimes

- runc - opencontainer runtime
- runv - hypervisorr-based runtime
- runhcs - Windows container host counterpart to runc
- runsc - gVisor runtime by Google
- kata-runtime - hypervisor-based runtime
- cc-runtime (deprecated) - hypervisor-based runtime

---
### Kubernetes - what is it?

> Kubernetes (K8s) is an open-source system for automating deployment, scaling, and management of containerized applications.
> 
> It groups containers that make up an application into logical units for easy management and discovery.

[kubernetes.io](https://kubernetes.io/)

+++
### Kubernetes Overview

![Kubernetes Components](https://d33wubrfki0l68.cloudfront.net/e298a92e2454520dddefc3b4df28ad68f9b91c6f/70d52/images/docs/pre-ccm-arch.png)

+++
### Glossary

- OCI - [Open Container Initiative](https://www.opencontainers.org/)(Image spec vs. Runtime spec)
    - Common runtimes: runc/runv/cc-runtime
- CNI - [Container Network Interface](https://github.com/containernetworking/cni#cni---the-container-network-interface) - network connectivity of containers
- CRI - Container Runtime Interface - K8s 1.5+ - Of the lowest layers of a Kubernetes node is the software that, among other things, starts and stops containers
- CSI - Container Storage Interface - K8s 1.9+ - standardized mechanism for Container Orchestration Systems (COs) to expose arbitrary storage systems to their containerized workloads
- [Pod Sandbox](https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/) - A Pod is composed of a group of application containers in an isolated environment with resource constraints

---
### Runtimes

CRI vs. OCI
