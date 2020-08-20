# Lab 1.1 Install Ansible and configure the controller

1.	Log into controller
2.	Using Putty SSH into your Ansible Controller - ___check credential details with instructure___

<span style="color:red">lin-ans01-student_number</span>

3.	Install EPEL-RELEASE

```
yum install epel-release -y
```

4.	Install Ansible, Git and Vim

```
yum install ansible git vim -y
```

5.	Run ```ansible –version```

Notice the ansible version, the default config file path and the python version being used
![](/images/ansible-version1.png)

6.	Clone the lab repo local
```
git clone git@github.com:mccbryan3/ansible_workshop_files.git
```
7. Change directories in the ansible_workshop_files directory
```
cd ansible_workshop_files
```
8. Cat the default-inventory file and verify
```
[win_nodes]
win-vm01-XX.youdomain

[lin_nodes]
lin-vm01-XX.yourdomain

[controllers]
lin-ans01-XX.yourdomain

[linux:children]
lin_nodes
controllers

[windows:children]
win_ndoes

[win_nodes:vars]
ansible_user=administrator
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore

[all:vars]
ansible_ssh_commen_args='-o StrictHostKeyChecking=no'
```
Be aware of the ini structure.<br>
Group variables are also specified in this file

7. Modify the default inventory file to specify your student number and change your to match the required FQDN for name resolution<br>
___If you do not have name resolution please notify the instructor to help specify ansible_host variable___

8. List hosts from the inventory file using --list-hosts  parameters

```
ansible all -i default-inventory --list-hosts
```

9. List groups of hosts in teh inventory file

```
ansible linux -i default-inventory --list-hosts

```

10. Run setup command on win_nodes hosts

Ansible adhoc commands are in the format below.<br>
```
ansible [inventory_pattern] -m [module] -a "[module options]"
```
We are also specifying the inventory file with the -i option
![](/images/lab1-winrm-error.png)

Notice the module error for winrm and requests

11.	Examine controller-config playbook
```
cat pb.controller-config.yaml
````
These tasks only run on localhost as specified at the top of the playbook
This will install our missing modules using pip.<br>
___hvac optional and may be removed___

![](/images/lab1-controller-config1.png)

Python modules installed here are pywinrm for windows machine support, pyvmomi for vmware support and hvac was included for secrets management with HashiVault.

12. Run the playbook
```
ansible-playbook controller-pre-reqs.yml
```
Examine the output
13. Rerun the setup command on the windows host group

```
ansible windows -i default-inventory -m setup
```
Examine the new message

![](/images/lab1.1-windows-ssl-pass-error.png)

Next we will configure credentials for connecting to the machines in the inventory

14. Copy your default-inventory file and name it inventory to make a "backup"

```
cp default-inventory inventory

**End of lab 1.1**

[Return to Main](/README.md)

