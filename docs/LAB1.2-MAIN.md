
# Lab 1.2 - Configure Credentials for Inventory Hosts

### Linux Configuration

Before you begin check you working directory. You should be in the root Domain-01.

```pwd``` should say ```/root/ansible_workshop_files/Domain-01```


1. Verify your inventory file is configured correctly and that the hostnames are resolvable or you have 'ansible_host=' variable set.

2. Open and view the lab_linux/pb.lab1.2-ansible-user.yaml file.

```vim lab_linux/pb.lab1.2-ansible-user.yaml```

The playbook starts with the play definition.

Then moves onto the tasks.

First we create the ansible-user while generating ssh keys for this user.

Then we move onto copying the local users public key into the authorized_keys file on the remote machines to enable passwordless remoting.

![](/images/lab1.2-ansible-user.png)

3. Run the playbook while specifying the root credentials as parameters to the ansible-playbook command.

First run the --syntax-check then run the playbook.<br>

The playbook should prompt for password of the root user.

***In this playbook we are configuring the ansible-user in the sudoers file to have access to run all commands wihtout a password prompt***

```
ansible-playbook -i inventory lab_linux/pb.lab1.2-ansible-user.yaml --user root --ask-pass --syntax-check

ansible-playbook -i inventory lab_linux/pb.lab1.2-ansible-user.yaml --user root --ask-pass
````

4. su into the ansible-user

```
su - ansible-user
```

5. Re-clone the github repo for the workshop as we will now be working as ansible-user

```
git clone https://github.com/mccbryan3/ansible_workshop_files.git
```

6. Use sudo and copy your inventory file to the ansible-user's directory

```
sudo cp /root/ansible_workshop_files/Domain-01/inventory /home/ansible-user/ansible_workshop_files/Domain-01
cd ansible_workshop_files/Domain-01/
```

6.1 Change owner and permissions on you inventory for the ansible-user

```
sudo chown ansible-user:ansible-user inventory
chmod 664 inventory
```

**Recheck your inventory file**

7. Run setup on the linux hosts to verify connectivity

```
ansible linux -i inventory -m setup
```

You should get a bunch of green and ansible_facts should fly by on your screen like so...<br>

![](/images/lab1.2-linux-setup.png)


**Configure privilege escalation variables for the linux ansible-user**

8. Create the group_vars directory and cd into the directory
```
mkdir group_vars
cd  group_vars
```

9. Create the file used for group varaibles (must be named after the group name)

```
vim linux.yaml
```

10. Enter the become variables required and write the file

```
---
ansible_become: True
```
11. Change directory back to the root of the project and examine pb.touchrootfile.yaml playbook.
```
cd ..
vim lab_linux/pb.touchrootfile.yaml
```
12. Quit the playbook without writing and run the playbook.

This playbook will attempt to create a file in the root users home directory to verify privilege escalation. 

```
ansible-playbook -i inventory lab_linux/pb.touchrootfile.yaml
```
The output should look like the following.

![](/images/lab1.2-touchroot1.png)

Verify that the newfile1 was created in the root home directory.

```ansible linux -a 'ls -l /root/' -i inventory```

![](/images/lab1.2-touchroot1-verify.png)

Assuming file exists in the root home diretctory as shown above, you are now using privilege escalation from ansible-user and becoming root on the hosts.

### Windows Configuration

Our Windows guests will need variable assignment for the username and password to use over winrm

There are a lot of options here however so we dont have to specify these in every playbook and so they also apply to the entire windwos host group we will be using group_vars in this case. Specifically located in the group_vars directory of the working project. We will also be using the dedicated file to encrypt our password using ansible-vault.

***Be sure you are in the ansible_workshop_files/Domain-01 directory***

1.	Create a file named after your inventory group.yml (windows.yml) and open it in an editor
```
vim group_vars/windows.yaml
````
3.	Add the windows ansible user credential variables to the file and save (stars should be replaced by your windows machine password)

![](/images/lab1.2-windows-vars.png)

4. Verify the credentials work for your lab box.

```
ansible windows -i inventory -m setup
```
Your output should be a large list of ansible_facts from the windows lab host.

Since our windows user credentials are now stored in plain text we will want to encrypt this file using [ansible-vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html)

5.	Run ansible-vault on the file to encrypt its contents and provide ‘password’ as the vault password (this would normally be something more secure)

```
ansible-vault encrypt group_vars/windows.yaml
New Vault password: 
Confirm New Vault password:
Encryption successful
```

6. Rerun your ansible setup module on the windows guests providing the --ask-vault-pass parameter

Provide the vault password when prompted and you should be given the windows ansible_facts again using the encrypted variable file.

```
ansible windows -i inventory -m setup --ask-vault-pass
```

![](/images/lab1.2-windows-setup.png)



**End of Lab1.2**

[Return to Main](/README.md)

