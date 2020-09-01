# LECTURE 1.4 - Ansible Playbook Syntax

### Playbook overiew

Put simply, playbooks are files containing Ansible plays. These plays are built for executing one or many tasks on Ansible inventory. The playbook is a way to develop advanced automation or configuration management tasks. There are multiple reasons for writing playbooks for automation, orchestration and configuration management tasks with just a few listed below.

* Allows you to easily make tasks reusable
* Integration into source control managment
* Ease of readability

Playbooks are written in YAML syntax. This allows for you to define your tasks in a declarative easy to read manner.

Playbooks are executed using the ```ansible-playbook``` binary.

Playbooks may contain many plays. 

Plays are defined by a play definition heading. 

The heading starts with... 

* The name of the play
    * This is most usually the purpose of the play and what it accomplishes.
* The host inventory the play is going to execute on
    * This can be a single host a group of hosts or **all** hosts 
    * These hosts must exist in the Ansible inventory
    
Some optional but often used play definition objects are privilege escalation with ```become:```. Considering that the playbook will run as the user executing ```ansible-playbook``` you may also define a user to execute the play as with ```remote_user:```. 

You may also define whether facts are gathered during play execution with ```gather_facts```. This is the default settings.

A simple play in a playbook may look like so...

```
- name: Show and example of a play
  hosts: windows
  remote_user: ansible-user
  become: yes
  gather_facts: yes
  
  tasks:
    
    - name: Create a file
      file:
        path: /root/newfile
        state: touch
```
