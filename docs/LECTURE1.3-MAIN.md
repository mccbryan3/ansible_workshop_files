# LECTURE1.3 - Create an examine an Ansible Configuration file

## ansible.cfg

During the previous labs we have been specifying the inventory file to which we were executing our playbooks. We also defined varibles for groups using the group_vars directory and variable file named after the groups. Along with many other parameters the ansible.cfg file can also hold some of this information related to the default behavior during play execution.

The ansible configuration file can be located in the following locations.

* ANSIBLE_CONFIG (env)
* /etc/anisble/ansible.cfg
* ~/ansible.cfg
* In the root of the “project” being ran (current directory)

For the most part your install should be fine using the default configuration file as most of the unique changes you would want to provide in external variables using the inventory file, group_vars, host_vars or playbook variables. Some of the parameters you might change exist in the default stanza. These include the path to the inventory file
and default forks but also can assist with saving other command line syntax.

![](/images/lecture1.3-ansible-cfg.png)

There are quite a bit of parameters in the ansible.cfg file and before you make modifcations understand that the changes here will apply to all of your plays. So be sure to test any modifications to your ansible.cfg file thoroughly and stick with placing variable changes closer to the plays being executed for more flexibility and easier troubleshooting.

More information on the ansible.cfg file can be found [here](https://docs.ansible.com/ansible/2.3/intro_configuration.html#)

## Inventory file

Plays for the most part are written to execute on remote hosts. These hosts are part of the inventory. Whether you are working with ansible engine or with Ansible Tower you will need to be familar with inventory.
