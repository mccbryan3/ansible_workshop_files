# LECTURE1.3 - Create an examine an Ansible Configuration file

During the previous labs we have been specifying the inventory file to which we were executing our playbooks. We also defined varibles for groups using the group_vars directory and variable file named after the groups. Along with many other parameters the ansible.cfg file can also hold some of this information related to the default behavior during play execution.

The ansible configuration file can be located in the following locations.

* ANSIBLE_CONFIG (env)
* /etc/anisble/ansible.cfg
* ~/ansible.cfg
* In the root of the “project” being ran (current directory)

For the most part your install should be fine using the default configuration file as most of the unique changes you would want to provide in external variables using the inventory file, group_vars, host_vars or playbook variables. Some of the parameters you might change exist in the default stanza. These include the path to the inventory file
and default forks but also can assist with saving other command line syntax.

![](/images/lecture1.3-ansible-cfg.png)
