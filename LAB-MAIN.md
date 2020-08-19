# Lab Main

Labs should be created on your own infrastructure. The lab should consist of the following.

* One ansible controller VM (centos8)
* One linux VM (centos8)
* One windows VM (windows 2019)

**We will be using CentOS Enterprise Linux in this lab. The lab will be tested with CentOS 8 using Ansible 2.9**

## Labs Content Summary
*	Variables
    * Syntax
    * Use cases
    * Register
*	Templating
    * Jinja Templating
    * Why its so awesome
*	Install Ansible
    * ansible-version
*	Check Python
    * python  -v
*	Pip
    * Pip install pyWinrm
    * Pip install pyvmomi
*	Ansible-Doc
    *	Snippets
*	Dissecting an ansible.cfg file
    *	locations
    *	basic parameters
    * ansible-config
*	Inventory File
    * Dissect inventory file
    * Dynamic Inventory
    * Host_Vars and Group_Vars
*	Ansible Adhoc Commands
    * -m <module> -a [<key=value>]
*	Dissecting a playbook
    *	hosts
    * vars and vars_files
    * secrets management
*	Ansible-Playbook
    * --syntax-check
    *	--check
    *	--extra-variables
*	Linux conf file Management with templates
    *	Chrony
    * Nfs-automount configuration
*	Linux software install
    * Yum Apt
*	Linux command and shell
    *	How to use and why not to use it
*	Windows Feature and DSC
    *	IIS
    *	SQL
*	Windows Registry and Files Management
    * Disable SSLv2
    * Enable Strict Name Checking
*	Windows win_command and win_shell
    * How to use and why not to use
*	vSphere VM Management
    * Build some VMs
    *	Configure a hosts adv config, time, cluster etc
*	Storage  management
    *	Basic Playbook arrangement
