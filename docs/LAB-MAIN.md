# Lab Main

## Requirements

**Labs should be created on your own infrastructure. The lab should consist of the following.**

* One ansible controller VM (centos8)
   * lin-ans01-XX
* One linux VM (centos8)
   * lin-vm01-XX
* One windows VM (windows 2019 - **WORKGROUP only - non domain joined**)
   * win-vm01-XX
   
**Currently the lab is being tested with Ansible 2.9.11**

The lab machines naming is very important. The names should be defined as shown above with the "XX" beign replaced by two digits starting from '01' and icrementing based on the number of students in the lab. This will line up directly to student numbers as we progeress through the labs.

example..

[student01]<br />
lin-ans01-01<br />
lin-vm01-01<br />
win-vm01-01

[student02]<br />
lin-ans01-02<br />
lin-vm01-02<br />
win-vm01-02

and so on....

**We will be using CentOS Enterprise Linux in this lab. The lab will be tested with CentOS 8 using Ansible 2.9**

## Labs Content Summary

These items will be installed and configured in the lab. The machines above should be fresh deployments before you begin.<BR>
___Do not install software or configure OS manually. We will doing this in the labs.___

### Install Ansible and configure the controller
* Install git
* Install vim
    * Configure vim for autoindent with yaml
*	Install Ansible
    * ansible-version
*	Check Python
    * python  -v
*	Pip
    * Pip install pyWinrm
    * Pip install pyvmomi

### Ansible install and directory structure
* What comes with the install and where is it at
    * /etc/ansible
    
### Ansible files
*	Dissecting an ansible.cfg file
    *	locations
    *	basic parameters
    * ansible-config
*	Inventory Files
    * Dissect inventory file
    * Dynamic Inventory
    * Host_Vars and Group_Vars*	Variables
    * Syntax
    * Use cases
    
### Playbook basics
*	Dissecting a playbook
    *	hosts
    * vars and vars_files
    * secrets management
* Ansible vault
    * Secrets Management

### Ansible commands brief
* Documentation with ansible-doc
*	Running Ansible Adhoc Commands
    * ansible <inventory> -m <module> -a [<key=value>]
*	Ansible-Playbook
    * --syntax-check
    *	--check
    *	--extra-variables

### Variables and Templating
* Variable basics
    * Jinja variables
    * Jinja common 
*	Templating
    * Jinja Templating
    * Why its so awesome
*	Linux conf file Management with templates
    *	Chrony
    * Nfs-automount configuration

### Basic linux playbooks
*	Linux software install
    * Yum Apt
*	Linux command and shell
    *	How to use and why not to use it

### Basic Windows Configuration and Playbooks
* Windows WIRM over https configuration
*	Windows Feature and DSC
    *	IIS
    *	SQL
*	Windows Registry and Files Management
    * Disable SSLv2
    * Enable Strict Name Checking
*	Windows win_command and win_shell
    * How to use and why not to use

## Optional Labs

**These labs require specialized infrastructure and will be avaialble for use only if your infrastcuture matches the lab**

*	vSphere VM Management
    * Build some VMs
    *	Configure a hosts adv config, time, cluster etc
* Storage Management
    * Basic playbook tasks

[Return to Main](/README.md)
