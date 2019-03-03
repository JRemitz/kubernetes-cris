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

@fa[question-circle fa-3x]
### Who’s testing their infrastructure (as code) and how?

+++
### Ansible Core on Testing...

[Ansible Testing Strategies](https://docs.ansible.com/ansible/latest/test_strategies.html)

> @size[22pt](Ansible believes you should not need another framework to validate basic things of your infrastructure is true. This is the case because Ansible is an order-based system that will fail immediately on unhandled errors for a host, and prevent further configuration of that host. This forces errors to the top and shows them in a summary at the end of the Ansible run...)

+++
