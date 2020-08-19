# Ansible Workshop – Ansible Playbook Basics

## Plays

Plays are defined by the specification of which inventory the play is set to execute, variables, and tasks and names. This playbook consists of YAML and is written in YAML tags. 
YAML starts with three dots and uses the yml or yaml extension in Ansible.

**Play structure**

![](/images/play-structure.png)

* Playbooks and YAML in general use a python type indentation to signify hierarchy.
* Playbooks may consists of multiple plays.
* Variables do not persist through plays.
* Playbooks will run by default as the executing user.

### Basic on Playbooks

**Plays are a collection of key value pairs. Keys in the same pair should share the same indentation. Playbooks are YAML files with the .yml file extension.

**Indentation is super important and the indention should be configured in vim. The indentation is based on two spaces.

___For better vim editing with yaml add the following to the ~/.vimrc file___

```
autocmd FileType yaml setlocal ai ts=2 sw=2 et
```
___you can use cursorcolumn to check indentation although I would save this for the command mode in vim___
```
set cursorcolumn
```
___Details on the autocmd___
```
#ai = auto indent<br>
#ts = tab stop<br>
#sw = Shift Width<br>
#et = expansetab<br>
```

* Check syntax before starting

ansible-playbook playbook.yml –syntax-check

* Dry run the playbook

ansible-playbook playbook.yml -C

-v for verbose.. Up to 4v's

ansible-playbook playbook.yml "-vvvv"

* Starts with three dashes "—" and can end with three dots "…"

Sample playbook with name, hosts and tasks

```
---
- name: Playbook description
  hosts: hosts
  tasks:
    - first
    - second
    - third
```
* Playbook tasks are ran in order

* Example playbook with task shown below

![](/images/playbook-example-task.png)

### "Print the output now" task details..

* Task uses the command module
* Registers the output of the module to the command_result variable
* Uses this variable to check the result and determine if it has failed

The second two register and **failed_when** are optional. These are best practice when working with the command module especially. Since the command module itself does not consider the command that is passed failing you will want to check the output for something to verify that the command succeeded or failed. You can also do something similar with **changed_when** for command and shell.

### Basic Tasks..

yum, copy, service, command, shell, etc……
```
ansible-doc task 
```
...for more information on tasks

### Playbooks can have multiple plays
```
- name
  hosts:
  tasks:
     -  task1_play1
- name
  hosts:
  tasks:
     - task1_play2
```
[Return to Main](/README.md)
