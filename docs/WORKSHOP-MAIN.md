# Ansible Workshop – Ansible Basics 

Prepared by: Bryan McClellan

This workshop is not to be considered all inclusive. The content here in should be considered enough to get the tools in your hands to start writing and maintaining your own playbooks.
This course assumes you have working knowledge of Linux and Windows Server Operating Systems and can work in a Linux text editor.

## Importance of Source Control Management
__Super Important__

## Basics
*	Controller Runs on Linux
*	Can manage all kinds of things
    * https://docs.ansible.com/ansible/latest/modules/list_of_all_modules.html
*	Agentless
*	Push Based - Pull with callback (Tower)
*	Desired State
*	Declarative
*	Modules are Idempotent
*	Ansible uses ssh for Linux and WinRm for Windows
*	Based on YAML files
*	Heavy use of Source Control
*	Built on order of precedence

## Terminology
*	Ansible
    * Ansible is an open-source software provisioning, configuration management, and application-deployment tool.[2] It runs on many Unix-like systems, and can configure both Unix-like systems as well as Microsoft Windows. It includes its own declarative language to describe system configuration. 
    * Ansible was written by Michael DeHaan and acquired by Red Hat in 2015. Ansible is agentless, temporarily connecting remotely via SSH or remote PowerShell to do its tasks.
*	Modules
    * Modules are written in standard scripting languages and are used to execute code either remotely or locally based on instructions set syntax provided in the modules.  These instructions are provided in the YAML syntax and written in the format described by the author of the module in the ansible-doc -s output.
* YAML
    * A markup language and also a data-oriented language that is considered more human readable than most languages. Python indentation (2 spaces), Perl based data types key value pair based. Used in configuration files and expressed in a colon-based style for key value pair assignment.
*	Playbook
    *	Playbooks are YAML files consisting of plays. Plays are instruction sets known as tasks gathered in a single file which specify information used to execute operations. The playbook contains information on where the operations of the tasks are to be performed as well as other play specific information. 
*	Tasks
    * Tasks are specified top to bottom in a play. These tasks use ansible modules or collections to execute specific operations on the hosts specified in the play. 
*	Inventory
    * Inventory consists of several hosts either provided as standalone hosts or grouped together using group tags in a file specified in the ansible.cfg file.
*	Roles
    * Roles are written using playbooks, tasks, variables and files in a specific directory structure. Roles are built to be used as reusable operations that may take many tasks and may also have conditions for operations. The goal of most reusable operations should be an Ansible Role. You can install and use collections through Ansible Galaxy
*	Collections
    * Collections are a distribution format for Ansible content that can include playbooks, roles, modules, and plugins. You can install and use collections through Ansible Galaxy.
*	Idempotent
    * Tasks should be written to be idempotent. Almost all modules are written to provide idempotency on the target host for the operation. Meaning the operation can be ran multiple times without performing the operation if it does not need to be performed. Essentially the tasks being ran can be ran multiple times and provide the same result. The exception to these are the command and shell modules.

## Important Files
* Ansible Config
    * File used to store parameters regarding the playbooks being executed
* Locations can be..
    * ANSIBLE_CONFIG (env)
    * /etc/anisble/ansible.cfg
    * ~/ansible.cfg
    * In the root of the “project” being ran (current directory)
*	Inventory
    * Default is located in /etc/ansible/hosts
    * List of hosts, groups and vars
    * Dynamic Inventory
* host_vars and group_vars
    * May be defined in the inventory file
    * Should be used in dedicated files in host and group var diretcories
      * Default location /etc/ansible/host_vars and /etc/ansible/group_vars
    * Group vars and host var files should be named the name of the group or host respectively and 

## Ansible Tower
*	Overview and use cases

## Links

**Docs**
https://docs.ansible.com/ansible/latest/index.html

**Galaxy**
https://galaxy.ansible.com/

**Ansible Sandbox**
https://github.com/mccbryan3/vagrant-ansible-sandbox

**Ansible Basics**
http://theopscorner.com/2019/10/ansible-playbook-basics/

### Bibliography
**There are no sources in the current document.**
* https://en.wikipedia.org/wiki/Ansible_(software)

