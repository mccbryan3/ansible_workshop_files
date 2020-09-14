# LECTURE 1.5 - Reviewing variables, jinja2 and conditionals

### Variable basics

As with any "scripting language" variables and working with variable is essential. Variables are used to asssign dynamic and transient data during the execution of your plays  and playbooks. 

It has already been discussed in the previous lectures how variable placement can determine the data that the variables hold based on.

Play based variables are usually assigned at the beginning of the play using the ```vars``` or ```vars_files``` or perhaps even the ```vars_prompt``` tags.

Variables in Ansible must begin with a letter and should only contain letters numbers and underscores. 

**Dashes/hyphens are not allowed**

Facts are also initialized with variables from the systems that the setup module is ran against.

The easiest way to see these variables is with the ```ansible locahost -m setup``` command.

### Simple variables

### Lists

### Dictionaries

### Jinja



