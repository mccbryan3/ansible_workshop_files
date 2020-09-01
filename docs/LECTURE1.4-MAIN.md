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

As stated earlier Playbooks are written in YAML syntax. YAML is dependent on indentation for interpretation.

Each indentation should be two spaces. I find most syntax errros when running playbooks stem from bad indentaton in the playbook.


