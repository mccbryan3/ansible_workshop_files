# LECTURE1.3 - Ansible configuration and Inventory Files

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

Plays for the most part are written to execute on remote hosts. These hosts are part of the inventory. Whether you are working with ansible engine or with Ansible Tower you will need to be familar with inventory. The default location for the inventory file is ```/etc/ansible/hosts```. As you have seen in the previous labs we have been specifying the path to our inventory file with the ```-i``` parameter on the command line. This is not a bad technque to use as it makes you fully aware of what inventory you are running your plays against. As you have seen above you can specify a unique inventory file using the ansible.cfg file to save typing on the command line.

### Defining inventory

The default inventory file is in and ini structure and I find this the easiest to work with so I use this structure throughout. The file can aslo be defined in YAML or JSON. Inventory is defined as either ungrouped or grouped hosts. All ungrouped hosts should be defined in the beginning of the file before any group stanzas.

In this lecture we will be using the default ansible inventory file to show how the file can be created.

Ungrouped or stand alone hosts are defined before any groups as shown below.

![](/images/lecture1.3-inventory-ungrouped.png)

Grouped hosts beloing to collection defined by a bracket stanza ```[group]```.

![](/images/lecture1.3-inventory-grouped.png)

Hosts may be defined using patterns. This is advantageous if you have many hosts that share the same naming convention but have numbers that increment them for uniqueness. This is done using the brackets as well but in the hostname itself.

![](/images/lecture1.3-inventory-pattern.png)

Any host defined should be contactable. That is either by the name defined as the host or by using an IP address as the host name.

All of the below definitions are correct if the ansible-controller can contact them be the defined names.

```
[servers]
server1
server1.domain.com
192.168.1.111
```

If you would like to use a name for a host but cannot resolve the name you can specify the ```ansible_host``` variable after the name to tell ansible to use that as the connection "name" for the host during play execution. Any host variable can be assigned in this manner by appending the variable inline.
```
server1 ansible_host=192.168.1.111
```

Groups can be members of groups as well using the ```[group:children]``` stanza. As you may have noticed in our lab we are adding groups into groups to allow us to run plays on a larger set or smaller set of host types.

![](/images/lecture1.3-inventory-children.png)

This allows us to use the ```[group:vars]``` to assign variables to our groups. This more likely would be something you would use in group_vars in your project but this is a valid place to use variables. In Ansible Tower group variables are assigned to the groups in the inventory and this is very much the same technique.

![](/images/lecture1.3-inventory-vars.png)

Dynamic inventory files can also be used to define inventory. These are usually scripts that define the inventory hosts and pull the inventory from a third-party solution including but not limited to AWS EC2 instances and VMware and other cloud and on-prem instances.

More information about dynamnic inventory can be found [here](https://docs.ansible.com/ansible/2.3/intro_dynamic_inventory.html)

All inventory should have the ability to be listed using the ```--list-hosts``` parameter from the command line.


[Lab-1.3](/docs/LAB1.3-MAIN.md)
