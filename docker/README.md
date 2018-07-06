## This is the Docker README which should give a high level overview of when to use Docker and when not to use it. 
I will like to have a number of use cases (examples) of using Docker.


#### What Docker is NOT any of the following:

Before we talk about what Docker is, I will talk about what it isn't. What is the negation of Docker? What are its limits? What can't Docker do?
- Docker is NOT a Linux Container technology (like LXC)
- Docker is NOT limited to just LXC anymore (can theoretically manage VMs in the future)
- Docker is NOT a Configuration Manager replacement (like Chef, Puppet, SaltStack, etc)
- Docker is NOT a PaaS
- Docker is NOT good at linking across separate servers or VMs (yet, see ambassadors)
- Docker is NOT good at isolating Linux Containers from each other (shared kernel)

However...

#### Docker IS the following:

- Docker is great at building and sharing disk images with others through the Docker Index
- Docker is a manager for infrastructure (today's bindings are for Linux Containers, but future bindings including KVM, Hyper-V, Xen, etc.)
- Docker is a great image distribution model for server templates built with Configuration * Managers (like Chef, Puppet, SaltStack, etc)
- Docker uses btrfs (a copy-on-write filesystem) to keep track of filesystem diff's which can be committed and collaborated on with other users (like git)
- Docker has a central repository of disk images (public and private) that allow you to easily run different operating systems (Ubuntu, Centos, Fedora, even Gentoo)

source: https://www.ctl.io/developers/blog/post/what-is-docker-and-when-to-use-it/

#### Tutorials


####
