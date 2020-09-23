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

1. Create a new file called pb.variables-<student number>.yaml
 <br> ___The example with student 01 below___

```vim pb.variables-01.yaml```

2. Enter the content shown below and save and exit the file.

![](/images/lab-1.5-playdefine-vars.png)

3. Check the Run the playbook syntax running the --syntax-check with ansible-playbook.

```ansible-playbook pb.variables-01.yaml --syntax-check```

4. Run the playbook
      * The playbook should prompt for the variable ```user``` based on the vars_prompt playbook key word.
<br>___output shown below___

![](/images/lab-1.5-play-out1.png)

5. Open the file again and add the highlighted portions from the graphic below.
   * This will add a list variable and give an example of looping through the list.

![](/images/lab-1.5-playdefine-vars-list.png)

6. Check the Run the playbook syntax running the --syntax-check with ansible-playbook.

7. Run the playbook and verify output.
<br>___Notice how the "Title" filter capatilizes the first letter in bryan.___

![](/images/lab-1.5-playdefine-vars-list01.png)

8. Create a new file in the current directory called template.j2 and enter the contents as shown in the image below.

![](/images/lab-template-j2.png)

9. Open the pb.variables-<student>.yaml file and enter the contents at the end of the playbook as shown in the image below.
 
![](/images/lab-template-task.png)

10. Check the Run the playbook syntax running the --syntax-check with ansible-playbook.

11. Run the playbook and verify output.

12. Cat the contents of the /home/ansible-user/template-test.txt file.

```cat /home/ansible-user/template-test.txt```
<br>___Notice how we used the for loop in Jinja to write the contents of the file based on Ansible variables.___

13. Add the below image contents to the pb.variables-<student>.yaml file at the bottom of the playbook.
 
 ![](/images/lab-facts-task.png)
 
14. Check the Run the playbook syntax running the --syntax-check with ansible-playbook.

15. Run the playbook and verify output.
 
 ![](/images/lab-facts-task-out.png)
 
 ___Notice how the task was skipped as we are on a RedHat os_family machine as localhost___
 
16. Modify the pb.variables-<student>.yaml file and change "Windows" to "RedHat" and rerun the playbook.

17. Verify that the output contains the ```ansible_facts['default_ipv4']``` facts








