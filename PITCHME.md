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

### Why?

- Lots of talks on Kubernetes and uses, little about how it works
- Many features within kubernetes to learn and understand for operations and architecture
- Grow awareness and begin focused discussions for community input/feedback

---
### Kubernetes Glossary

- CRI - Container Runtime Interface
- CNI - Container Network Interface
- CSI - Container Storage Interface
- OCI - Open Container Initiative(Image spec vs. Runtime sepc)
- runc/runv/cc-runtime
- Pod Sandbox

+++
### Kubernetes Overview

![Kubernetes Components](https://d33wubrfki0l68.cloudfront.net/e298a92e2454520dddefc3b4df28ad68f9b91c6f/70d52/images/docs/pre-ccm-arch.png)

