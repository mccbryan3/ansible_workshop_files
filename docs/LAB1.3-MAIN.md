# LAB 1.3 - Exploring the ansible.cfg and Inventory files

Create and ansible,cfg file in the working project directory and create a vault_password_file.

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
Copy the default lab ansible.cfg into the Domain-01 project directory and open it for editing.

```
cp ../ansible.cfg .
vim ansible.cfg
```

Uncomment the inventory definition and change it to point to the inventory file in the project directory as shown below. 

![](/images/lab1.3-default-inv.png)

Locate the ```vault_password_file``` defintion in the file using the vim search function ```/``` from the command mode by pressing ESC a couple times.

___You should take some time to familiarize yourself with the vi and vim editors for the labs. If you are not familiar I highly recommend taking some time and learning some basic commands using a quick reference [references(https://www.adminschoice.com/vi-editor-quick-reference)___

Modify the entry to use a file named vault_password_file in the ansible-user's home directory as shown below.

![](/images/lab1.3-vault_file.png)

Exit and save the file.

Create the vault_password_file and place **only the password you used to encrypt the windows.yaml group_vars file** in lab1.2.

The file should contain one line and that is the password used to encrypt the file.

```
vim ~/vault_password_file
```

Exit and run the ```ansible-inventory all --list``` command.

The results should be a list of your inventory including all variables and the password for your windows group should be in the output.

Play around listing the inventory using the ``ansible`` ad-hoc command.

![](/images/lab1.3-list-inv.png)


**End lab1.3**

Return to Main


**End of Lab1.3**

[Return to Main](/README.md)
