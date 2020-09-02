# LECTURE 1.4 - Ansible Playbook Syntax

### Playbook overiew

Put simply, playbooks are files containing Ansible plays. These plays are built for executing one or many tasks on Ansible inventory. The playbook is a way to develop advanced automation or configuration management tasks. There are multiple reasons for writing playbooks for automation, orchestration and configuration management tasks with just a few listed below.

* Allows you to easily make tasks reusable
* Integration into source control managment
* Ease of readability

Playbooks are written in YAML syntax. This allows for you to define your tasks in a declarative easy to read manner.

* Playbooks and YAML in general use a python type indentation to signify hierarchy.
* Playbooks may consists of multiple plays.
* Variables do not persist through plays.
* Playbooks will run by default as the executing user.

Playbooks are executed using the ```ansible-playbook``` binary.

Playbooks may contain many plays. 

## Play structure

The below playbook shows, graphically the basic structure of a playbook.

![](/images/play-structure.png)

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
  hosts: linux
  remote_user: ansible-user
  become: yes
  gather_facts: yes
  
  tasks:
    
    - name: Create a file
      file:
        path: /root/newfile
        state: touch
```

In this example we...

* Name the play
* Define the hosts that the play will execute on
* Use become for privilege escalation
* Use the ansible-user account to execute the play on the remote hosts
* Confirm that we want to gather facts
* Define our tasks heading
* Define a task using the file module to create a file

### Playbooks can have multiple plays

A multiple play playbook could look something like the below.

```
- name: Touch a file in the root home dir
  remote_user: ansible-user
  become: yes
  hosts: linux
  gather_facts: yes

  tasks:
    - name: Do the touching
      file:
        state: touch
        path: /root/newfile1

- name: Configure firewall for Windows
  hosts: win_nodes
  gather_facts: yes

  tasks:

    - name: Open ICMP port
      win_firewall_rule:
        name: ICMP Allow incoming V4 echo request
        enabled: yes
        state: present
        action: allow
        direction: in
        protocol: icmpv4
```

In the playbook above we have two plays defined. One play runs on the linux group and the second runs on a windows group. Each play has a set of play definitions to allow the play to execute as expected.

### Basic file editing for playbooks

**Plays are a collection of key value pairs. Keys in the same pair should share the same indentation. Playbooks are YAML files with the .yaml file extension.**

**Indentation is super important and the indention should be configured in vim. The indentation is based on two spaces.**

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

```ansible-playbook playbook.yml –syntax-check```

* Dry run the playbook

```ansible-playbook playbook.yml -C```

-v for verbose.. Up to 4v's

```ansible-playbook playbook.yaml -vvvv```

* YAML starts with three dashes "—" and can end with three dots "…"

* Playbook tasks are ran in order

* Example playbook with task shown below

![](/images/playbook-example-task.png)

### "Print the output now" task details..

* Task uses the command module
* Registers the output of the module to the command_result variable
* Uses this variable to check the result and determine if it has failed

The second two register and **failed_when** are optional. These are best practice when working with the command module especially. Since the command module itself does not consider the command that is passed failing you will want to check the output for something to verify that the command succeeded or failed. You can also do something similar with **changed_when** for command and shell.

### Basic Tasks..

yum, copy, service, command, shell, etc…

windows modules usually start with the "win_" prefix.

Use the ```ansible-doc``` command on specific modules to get information about the module. 

The ansible-doc command can also be ran with the ```-s``` parameter to get a "snippet" exmaple of the modules usage.

```
ansible-doc module
```
Let's head to lab 1.4 to write a playbook or two.

[Lab 1.4](/docs/LAB1.4-MAIN.md)
