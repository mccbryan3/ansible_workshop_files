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

Simple variables are declared and defined as follows.

```
vars:
  simple_var1: some_variable1
```

Variables can be accessed in your ansible playbooks using the Jinja style variable syntax.

```"{{ simple_var1 }}"```

These variables can also be provided during the playbooik execution using the ```--extra-vars``` or ```-e``` parameter which can provide variables to the playbook or ad-hoc ansible command at execution. **The variables provided with the command line ```-e``` will also overwrite any variables that are provided in the playbook with the same name.**

Variable precendence order is listed below with the higher number listed overwriting any previous variables that are defined.

1. Configuration settings
2. Command-line options
    * used primarily for become, user etc and not related to extra-vars
3. Playbook keywords
4. Variables
5. Extra Variables

Due to variable precedence it is a good practice to develop a method for providing varaibles to playbooks and sticking with that method.

```
- name: variables all over
  hosts: localhost
  vars:
    sample_var1: variable_content
  tasks:
    
    - debug:
        msg: "Echoing out the variable : {{ sample_var1 }}"
      vars:
        sample_var1: replace_content
```

In the play above the variable ```sample_var1``` has defined at the play as a play keyword and then subsequently overwritten at  the task level.

Running the playbook will yield the following output.

```
TASK [debug] *************************************
ok: [localhost] => {
    "msg": "Echoing out the variable : replace_content"
}
```

Even further you could replace this variables at the command line with the 

```ansible-playbook overwritten-vars.yaml -e "sample_var1=overwrtten_content"```

Which will yield the output.

```
TASK [debug] *************************************
ok: [localhost] => {
    "msg": "Echoing out the variable : overwrtten_content"
}
```

### Lists

Variables can contain lists of items sometimes called arrays in other languages.

Lists are defined simply by provided by providing each **item** in the list under the variable prefixed with the dash and a space.

```
  var_test2:
    - item1
    - item2
    - item3
```

Lists can be used in many ways in Ansible with the primary purpose of looping through items in a task. The below example shows a task using the list with the **with_items:** module and applying each item to the debug module task.

```
  - name: Looping through list variable
    debug:
      msg: "{{ item }}"
    with_items: "{{ var_test2 }}"
```

It is worth noting that the ```"{{ item }}"``` assumes the default variable status of each item in the list. The output of the above task with the list provided will is shown below. As you can see in the Ansible playbook output the "{{ item }}" simply becomes each variable in the list as shown with the **item=item1** output.

```
TASK [Looping through list variable] ***********************************
ok: [localhost] => (item=item1) => {
    "msg": "item1"
}
ok: [localhost] => (item=item2) => {
    "msg": "item2"
}
ok: [localhost] => (item=item3) => {
    "msg": "item3"
}
```

Defining an empty list can be done using the following syntax.

```list_variable: []```

### Dictionaries

Dictionaries in Ansible are key value pairs and can also be defined as variables and provide a mechanism for referencing data.

Dictionary variables are defined with the curly braces ```{}```. An example of a dictionary variable being defined is shown below.

```
var_dict:
  { item_key1: value1, item_key2: value2, item_key3: value3 }
```

A task using these can access the key name and the value by using the ```with_dict:``` module and the same technique as the list however using the **item.key** and **item.value** as shown in the example below.

```
  - name: Dictionary variables
    debug:
      msg: "Item key is {{ item.key }} and the value is {{ item.value }}"
    with_dict: "{{ var_dict }}"
```

The output of the above task with the previosly defined dictionary items is show below.

```
TASK [Dictionary variables] ********************************************************
ok: [localhost] => (item={'key': 'item_key1', 'value': 'value1'}) => {
    "msg": "Item key is item_key1 and the value is value1"
}
ok: [localhost] => (item={'key': 'item_key2', 'value': 'value2'}) => {
    "msg": "Item key is item_key2 and the value is value2"
}
ok: [localhost] => (item={'key': 'item_key3', 'value': 'value3'}) => {
    "msg": "Item key is item_key3 and the value is value3"
}
```

A great way to learn to work with variable types is by exploring the Ansible facts using the **setup** module. Ansible facts are variables gathered from hosts during playbook execution if **gather_facts** is set to yes (the default). These are special variables used for accessing host information in Ansible to help make decisions using conditionals in Ansible playbooks. All of these facts are prefaced with **ansible_**.

Facts can be accessed by walking the fact "tree" using the square brackets.

Two examples of accessing ansible facts are shown below.

The below returns all ipv4 addresses from the host.

```"{{ ansible_facts['all_ipv4_addresses'] }}"```

The below fact uses the date_time fact from the host and accesses the value of the vaaue of the iso8601 key from the date_time dictionary. This is an example of accessing nested variables.

```{{ ansible_facts['date_time']['iso8601'] }}```

I encourage using the Ansible facts to help learn how to work with variables and explore different variable types.

### Jinja2 Templating

The "{{ }}" brackets are part of the Jinja2 templating language used heavily in Ansible.

Jinja also uses **filters** heavily to transform data. Jinja filters are applied in the following format.

```"{{ variable | filter }}"```

The list of Jinja filters is vast and could probably take a workshop in itself. I have compiled a list of some of, what I consider, the most widely used Jinja2 filters below with examples.

1. Changes the variable to all UPPERCASE

```"{{ variable | upper }"```

2. Changes the variable to all lowercase

```"{{ variable | lower }"```

3. Math functions work in Jinja

```"{{ 13.4 * 53 }}"```

4. Setting the default for variables. This is helpful when used in playbooks where the variable may never be defined.
    * Playbooks will stop and errror on undefined variables so setting defaults may be helpful on those occasions for dealing with undefined variables
    * This example sets the variable ```variable``` to "hey there" if it is not defined anywhere else.

```"{{ variable | default("hey there") }}"```

5. Complex loops. This example simply loops through the var_test2 variable and is similar to the with_items used above with lists however is much more useful in templating for configuration files.

```"{% for item in var_test2 %} {{ item }} {% endfor %}"```

6. Use the below type_debug filter to get the data type of the variable.

```{{ variable | type_debug }"```

More on Jinja2 filters used in Ansible can be found [here](https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html)

### Conditionals and Register

Playbook conditionals are used to make decisions in plays and on tasks. All conditionals rely on ansible facts or variables when making decsisions and ultimately control the flow of your plays and playbooks.

When executing tasks you can set the result of that task to a variable on the end of the task usng the **register** module.

This allows you to make further decisions in your play on the contents of that task result or use that data from subsequent tasks.

Example of the using register with a task and taking the stdout of the command module and displaying the output.

The variable ```where_is_password``` is filled by the shell module using the ```group -R password .``` command which looks in all files in the current directory recursively and captures all of the output. The command module is a dictionary output by default with the standard output stored in the stdout key. We access the value of the key with the ```.``` as used similar to object oriented languages as properties.

```
  - name: Find all files with the word password in the current directory
    shell: "{{ command }}"
    vars:
      - command: "grep -R 'password' ."
    register: where_is_password

  - name: debug where_is_password
    debug:
      msg: "{{ where_is_password.stdout }}"
      
```



