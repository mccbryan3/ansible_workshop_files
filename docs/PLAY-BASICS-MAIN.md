# Ansible Workshop – Ansible Playbook Basics

## Plays

Plays are defined by the specification of which inventory the play is set to execute, variables, and tasks and names. This playbook consists of YAML and is written in YAML tags. 
YAML starts with three dots and uses the yml or yaml extension in Ansible.

**Play structure**

![](/images/play-structure.png)

- Playbooks and YAML in general use a python type indentation to signify hierarchy.
- Playbooks may consists of multiple plays.
- Variables do not persist through plays.
- Playbooks will run by default as the executing user.

