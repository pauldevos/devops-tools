# DevOps Tools

Testing and installing of Python environments and packages.
- Tox
- Pytest
- CircleCI (or TravisCI, Jenkins)
- 

- [Continuous Integration](https://realpython.com/python-continuous-integration/)

https://www.heavybit.com/library/blog/opinionated-tour-of-testing-tools/


### Commit Hooks
- [Pre-Commit](https://pre-commit.com/)

# devops-tools-repository
This will serve as a reservoire of [public] notes for me that outline various "infrastucture as code" thoughts and tools I've tried. I'll probably curate a number of articles that also helped shape this process.

DevOps has a crap-ton of tools. If you want your mind blown, just go here and look around [DevOpsBookMarks](http://www.devopsbookmarks.com/). A truly exhaustive resource on the number of tools out there.




#### DevOps - DataOps Categories

- Configuration Management
- Environment Management
- Package Management
- Infrastructure Management
- Software Provisioning
- Application Deployment

There are different types of tools that `manage` variable parts of the provisioning, configuring, envrionment, packaging, and deployment processes. This is a table to help identify which tool can do what. It does not necessarily take into account the difficulty for each category (that may come later as I understand each tool more). 

|Tool | Orchestration | Configuration| Environment| Infrastructure|Install Software | App Deployment | Package|
| ------------- | :--------:  | :--------:  |:--------:| :--------: | :--------:  | :--------: | :--------: |
| [Ansible](https://www.ansible.com/)| Yes |Yes | Yes| Very Well| No | Yes | Sort of |
| [Kubernetes](https://kubernetes.io/) | - | - |  - | - | - | - | - |
| [Docker](https://www.docker.com/what-docker) | No | Yes | No | No | Yes| No | No |
| [Terraform](https://www.terraform.io/docs/index.html)| Yes | - | - | - | - | - | - |
| CloudFormation | Yes | - | - | - | - | - | - |
| [Packer](https://www.packer.io/intro/index.html) | Yes | - | - | - | Yes | - | - |
| [Chef](https://www.chef.io/)| Yes | - | Yes | - | - | - | - |
| [Puppet](https://puppet.com/) | Yes | - | Yes | - | - | - | - |
| [SaltStack](https://saltstack.com/community/) | Yes | - | Yes | - | - | - | - |
| [Fabric](http://www.fabfile.org/) | Yes | Yes | - | - | - | - | - |






Odd stuff....

- [Stack Overflow - How can I test jinja2 templates in ansible?](https://stackoverflow.com/questions/35407822/how-can-i-test-jinja2-templates-in-ansible)
- [Shell Scripts to Ansible](https://www.ansible.com/blog/shell-scripts-to-ansible)


Kubernetes
  - [Airflow on Kubernetes - Part 1](https://kubernetes.io/blog/2018/06/28/airflow-on-kubernetes-part-1-a-different-kind-of-operator/)
  - [A Friendly Introduction to Kubernetes](https://medium.freecodecamp.org/a-friendly-introduction-to-kubernetes-670c50ce4542)
  - [Docker Development Workflow](https://medium.freecodecamp.org/docker-development-workflow-a-guide-with-flask-and-postgres-db1a1843044a)
