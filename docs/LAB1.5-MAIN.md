# LAB 1.5 - Writing playbooks with variables and conditionals

Write playbooks using variables and conditonals

Verify your working directory is Domain-01.

```
pwd
whoami
```

If not su into ansible-user and cd into the working directory.

```
su - ansible-user
cd /home/ansible-user/ansible_workshop_files/Domain-01
```

1. Create a new file called **pb.variables-<student number>.yaml**
 <br> ___example with student 01 below___

```vim pb.variables-01.yaml```

2. Enter the content shown below and save and exit the file.

![](/images/lab-1.5-playdefine-vars.png)

3. Check the Run the playbook syntax running the --syntax-check with ansible-playbook.

```ansible-playbook pb.variables-01.yaml --syntax-check```

4. Run the playbook
      * The playbook should prompt for the variable ```user``` based on the vars_prompt playbook key word.
<br>___output shown below___

![](/images/lab-1.5-play-out1.png)

5. 


