# Ansible

Ansible is often described as a _`configuration management`_ tool, and is typically mentioned in the same breath as Chef, Puppet, and Salt. When we talk about configuration management, we are typically talking about **writing some kind of state description for our servers, and then using a tool to enforce that the servers are, indeed, in that state: the right packages are installed, configuration files contain the expected values and have the expected permissions, the right services are running, and so on.** Like other configuration management tools, Ansible exposes a domain-specific language (DSL) that you use to describe _the state_ of your servers. 

These tools can be used for deployment as well. When people talk about _`deployment`_, they are usually referring to the **process of taking software that was written in-house, generating binaries or static assets (if necessary), copying the required files to the server(s), and then starting up the services.** _Capistrano_ and _Fabric_ are two examples of open source deployment tools. Ansible is a great tool for `deployment` as well as `configuration management`. Using a single tool for both configuration management and deployment makes life simpler for the folks responsible for operations. 

Some people talk about the need for _`orchestration of deployment`_. This is where **multiple remote servers are involved, and things have to happen in a specific order.** For example, you need to bring up the database before bringing up the web servers, or you need to take web servers out of the load balancer one at a time in order to upgrade them without downtime. Ansible is good at this as well, and is designed from the ground up for performing actions on multiple servers. **Ansible has a refreshingly simple model for controlling the order in which actions happen.** 

Finally, you’ll hear people talk about _`provisioning`_ new servers. In the context of public clouds such as Amazon EC2, this refers to spinning up a new virtual machine instance. -- _`Ansible: Up and Running`_


Putting It All Together 

To sum up, a `playbook` contains one or more `plays`. A `play` associates an unordered set of `hosts` with an ordered list of `tasks`. Each `task` is associated with exactly one `module`. 

The figure below is an entity-relationship diagram that depicts this relationship between playbooks, plays, hosts, tasks, and modules.

<p align="center">
  <img src="https://github.com/pauldevos/devops-tools/blob/master/ansible-playbooks.png?raw=true" alt="Playbooks Image"/>
</p>

### Ansible Playbook

```bash 
# web-notls.yml
- name: Configure webserver with nginx
  hosts: webservers
  become: True
  tasks:
    - name: install nginx
      apt: name=nginx update_cache=yes

    - name: copy nginx config file
      copy: src=files/nginx.conf dest=/etc/nginx/sites-available/default

    - name: enable configuration
      file: >
        dest=/etc/nginx/sites-enabled/default
        src=/etc/nginx/sites-available/default
        state=link

    - name: copy index.html
      template: src=templates/index.html.j2 dest=/usr/share/nginx/html/index.html
        mode=0644

    - name: restart nginx
      service: name=nginx state=restarted
```



### Ansible Configuration
- This comes in handy when you're trying to set up or tweak your Ansible configuration.


`ansible-config` utility allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. See [ansible-config](https://docs.ansible.com/ansible/latest/cli/ansible-config.html#ansible-config) for more information.


```bash
ansible-config [view|dump|list] [--help] [options] [ansible.cfg]
```

- [Ansible Config Variables](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#ansible-configuration-settings)


### Useful Command Line Tools ([Link](https://docs.ansible.com/ansible/latest/user_guide/command_line_tools.html))

### ansible <host-pattern>
  
```bash
ansible <host-pattern> [options]

[options]
--list-hosts

-C, --check # doesn’t make any changes; instead, try to predict some of the changes that may occur

-D, --diff # when changing (small) files and templates, show the differences in those files; works great with –check

-i, --inventory # specify inventory host path or comma separated host list. –inventory-file is deprecated

-m <MODULE_NAME>, --module-name <MODULE_NAME> # module name to execute (default=command)
```

### ansible-config

```bash
ansible-config [view|dump|list] [--help] [options] [ansible.cfg]

-c <CONFIG_FILE>, --config <CONFIG_FILE>

list
list all current configs reading lib/constants.py and shows env and config file setting names

dump
Shows the current settings, merges ansible.cfg if specified

--only-changed
Only show configurations that have changed from the default

view
Displays the current config file
```

### ansible-console
  
```bash
ansible-console [<host-pattern>] [options]

-C, --check # don’t make any changes; instead, try to predict some of the changes that may occur

-D, --diff # when changing (small) files and templates, show the differences in those files; works great with –check
```

### ansible-inventory
```bash
ansible-inventory [options] [host|group]

-- export # When doing an –list, represent in a way that is optimized for export,not as an accurate representation of how Ansible has processed it

-- graph # create inventory graph, if supplying pattern it must be a valid group name

-- list # Output all hosts info, works as inventory script
```

### ansible-playbook

The `ansible-playbook` command executes playbooks. 

```bash
ansible-playbook [options] playbook.yml [playbook2 ...]

--flush-cache # clear the fact cache for every host in inventory

--force-handlers # run handlers even if a task fails

--list-hosts # outputs a list of matching hosts; does not execute anything else

--list-tags # list all available tags

--list-tasks # list all tasks that would be executed

--syntax-check # perform a syntax check on the playbook, but do not execute it

-C, --check # don’t make any changes; instead, try to predict some of the changes that may occur

-D, --diff # when changing (small) files and templates, show the differences in those files; works great with –check

-i, --inventory, --inventory-file # specify inventory host path or comma separated host list. –inventory-file is deprecated
```

