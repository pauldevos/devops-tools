# Ansible


### Ansible
- This comes in handy when you're trying to set up or tweet your Ansible configuration.


`ansible-config` utility allows users to see all the configuration settings available, their defaults, how to set them and where their current value comes from. See [ansible-config](https://docs.ansible.com/ansible/latest/cli/ansible-config.html#ansible-config) for more information.


```bash
ansible-config [view|dump|list] [--help] [options] [ansible.cfg]
```

- [Ansible Config Variables](https://docs.ansible.com/ansible/latest/reference_appendices/config.html#ansible-configuration-settings)


### Useful Command Line Tools ([Link](https://docs.ansible.com/ansible/latest/user_guide/command_line_tools.html))

- ansible <host-pattern>
```bash
ansible <host-pattern> [options]

[options]
--list-hosts

-C, --check # doesn’t make any changes; instead, try to predict some of the changes that may occur

-D, --diff # when changing (small) files and templates, show the differences in those files; works great with –check

-i, --inventory # specify inventory host path or comma separated host list. –inventory-file is deprecated

-m <MODULE_NAME>, --module-name <MODULE_NAME> # module name to execute (default=command)
```

- ansible-config
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

- ansible-console
  
```bash
ansible-console [<host-pattern>] [options]

-C, --check # don’t make any changes; instead, try to predict some of the changes that may occur

-D, --diff # when changing (small) files and templates, show the differences in those files; works great with –check
```

- ansible-inventory
```bash
ansible-inventory [options] [host|group]

-- export # When doing an –list, represent in a way that is optimized for export,not as an accurate representation of how Ansible has processed it

-- graph # create inventory graph, if supplying pattern it must be a valid group name

-- list # Output all hosts info, works as inventory script

