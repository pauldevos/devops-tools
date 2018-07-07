# tools-repository
A repository of tools used for Data Science, Machine Learning, Deep Learning, Data Engineering, and DataOps revolving around reproducibility and compatability across operating systems

## Tools

Repositories
- Github
- Bitbucket
- Gitlab
  - Why I choose Github? Popularity and 3rd party extensions
 

CI/CD
- CircleCI
- TravisCI

Jupyter Hub

Docker Hub

## Deployment


This is an effort on my part to understand and share what tools do what within the deployment process.

#### Documentation Method #1
- Configuration Management
  - Chef, Puppet, SaltStack, Ansible
- Environment Management
- Package Management
- Infrastructure Management
  - Docker
- Software Provisioning
  - Ansible
- Application Deployment
  - Ansible
  
#### Documentation Method #2

Categories:
- Configuration Management
- Environment Management
- Package Management
- Infrastructure Management
- Software Provisioning
- Application Deployment

Chef
* Configuration Management
  
Puppet
* Configuration Management
  
SaltStack
* Configuration Management

Teraform - [Use Cases](https://www.terraform.io/intro/use-cases.html)

Ansible
* Configuration Management
* Software Provisioning
* Application Deployment
* Orchestration Manager
  
#### Documentation Method #3

- Configuration Management
- Environment Management
- Package Management
- Infrastructure Management
- Software Provisioning
- Application Deployment

There are different types of tools that `manage` variable parts of the provisioning, configuring, envrionment, packaging, and deployment processes. This is a table to help identify which tool can do what. It does not necessarily take into account the difficulty for each category (that may come later as I understand each tool more). 

|Tool | Orchestration | Configuration| Environment| Infrastructure|Software | Application Deployment | Package|
| ------------- |------------- | ------------- |:-----------:| --------:       |------------- |:-----------:| --------:|
| Ansible | Yes |Yes | Yes       | Very Well           | No     | Yes       | Sort of    |
| Kubernetes | col 2 is      |col 2 is      | centered    |   $12           |col 3 is      | right       | $1600    |
| Docker | zebra stripes |zebra stripes | are neat    |    $1           |col 3 is      | right       | $1600    |
| Terraform | Yes |zebra stripes | are neat    |    $1           |col 3 is      | right       | $1600    |
| CloudFormation | Yes |zebra stripes | are neat    |    $1           |col 3 is      | right       | $1600    |


Configuration management tools install and manage software on servers that are provisioned. Some examples of configuration management 
tools include Chef, Puppet, Ansible, and SaltStack. 

> These two categories [orchestration and configuration management] are not mutually exclusive, as most configuration management tools can do some degree of provisioning and most 
> orchestration tools can do some degree of configuration management. But the focus on configuration management or orchestration means
> that some of the tools are going to be a better fit for certain types of tasks. - [Yevgeniy Brikman](https://blog.gruntwork.io/why-we-use-terraform-and-not-chef-puppet-ansible-saltstack-or-cloudformation-7989dad2865c)
  
- Chef, Puppet, SaltStack, Ansible

Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates.

Ansible is an open source software that automates software provisioning, configuration management, and application deployment

In contrast with popular configuration management software — such as **Chef**, **Puppet**, and **CFEngine** — **Ansible** uses an 
*agentless* architecture. With an *agent-based* architecture, nodes must have a locally installed daemon that communicates with a controlling
machine. With an  agentless architecture, nodes are not required to install and run background daemons to connect with a controlling 
machine. This type of  architecture reduces the overhead on the network by preventing the nodes from polling the controlling machine.

source: [Wikipedia](https://en.wikipedia.org/wiki/Ansible_(software))


#### Configuration Management

#### Python Environment Management
- Conda
- Pyenv
- venv
- virtualenv
- ?

#### Python Package Management
- Conda
- pip
- ?





[Helm](https://github.com/kubernetes/helm) - a Kubernetes Package Manager

Kubernetes
  - [Airflow on Kubernetes - Part 1](https://kubernetes.io/blog/2018/06/28/airflow-on-kubernetes-part-1-a-different-kind-of-operator/)

Ansible

Chef

Puppet

Jenkins

## Workflow Schedulers, Monitors

[Airflow](https://airflow.apache.org/)
- Redis
- Postgres
- Celery

## Web Development

Python Web Frameworks
- Flask
- Django
- Tornado

Blog/CMS
- Pelican
- Wagtail


## Big Data Engineering
Spark
- PySpark
- Scala
- Performance Tuning

Dask
Pandas on Ray


Unit Testing
- pytest
- unittest
- nose

Text Editors
- Sublime
- Atom
- Nano
- Vi/Vim/Emacs

IDEs
- PyCharm

## Cloud Provisioning

AWS
- CloudFormation
- S3
- EC2
- RDS
- RedShift
- Aurora

GCP
- Cloud Storage
- Cloud SQL
- Compute Engine
- BigQuery
- Cloud Spanner




## Machine Learning

Machine Learning Algorithms
- Linear Regression
- Logistic Regression
- Decision Trees
- K-Nearest Neighbors (KNN)
- K-Means
- Support Vector Machines (SVM)
- Principal Component Analysis (PCA)
- Gradient Boost
- Neural Networks
  - CNN
  - GNN

## Deep Learning

#### Might Put these in a separate repo README (and folder) or just leave this folder as the "link farm"
Artificial Intelligence Fundamentals:
- Algebraic concepts
- Linear Algebra
- Optimization Methods
- Numerical Algorithms
- Feature Selection
- Project Structure
  - Vectorization of Data
  - Feature Engineering
  - Handling missing data and outliers, imputation
  - Train/Validation/Test
  - Metrics


## Databases (non-cloud)
- ElasticSearch
- Postgres
- Redis
- TimeScaleDB
- MongoDB
- Cassandra
- Neo4J

Python
- OOP (practices)
  - Types of Classes: Static, Method, Data, etc
  - Decorators
  - 4 Pillars
  - etc
- FP (practices)

- Security
  - SSH
  - VPN
  - Ports
  - PHI/PII
  - HiTRUST
  - other?

Above would link to links in format below
---- 

#### Github
Lays out understanding, tutorial, etc
Branching, Merging, Pull, Push, etc
Multiple Accounts on same computer

Cheatsheet of commands:
    - command_1
    - command_2
    - command 3
Other helpful resources:
  - subLink #1 
  - subLink #2
  - subLink #3


#### Python Environment Management
  - Link #1
  - Link #2
  - Link #3
  - Cheatsheet of commands:
    - command_1
    - command_2
    - command 3
  
  
  
Python Package Management
- tool #1
- tool #2
- tool #3

