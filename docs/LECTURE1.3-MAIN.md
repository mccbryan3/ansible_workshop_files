# LECTURE1.3 - Create an examine an Ansible Configuration file

During the previous labs we have been specifying the inventory file to which we were executing our playbooks. We also defined varibles for groups using the group_vars directory and variable file named after the groups. Along with many other parameters the ansible.cfg file can also hold some of this information related to the default behavior during play execution.

The ansible configuration file can be located in the following locations.

* ANSIBLE_CONFIG (env)
* /etc/anisble/ansible.cfg
* ~/ansible.cfg
* In the root of the “project” being ran (current directory)