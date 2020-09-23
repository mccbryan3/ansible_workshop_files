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

Simple variables are created and assigned as follows.

```
vars:
  simple_var1: some_variable1
```

Variables can be accessed in your ansible playbooks using the Jinja style variable syntax.

```"{{ simple_var1 }}"```

These variables can also be provided during the playbooik execution using the ```--extra-vars``` or ```-e``` parameter which can provide variables to the playbook or ad-hoc ansible command at execution. **The variables provided with the command line ```-e``` will also overwrite any variables that are provided in the playbook with the same name.**

Due to variable precedence it is a good practice to develop a method for providing varaibles to playbooks and sticking with that method.


### Lists

### Dictionaries

### Jinja Templating

### Conditionals
