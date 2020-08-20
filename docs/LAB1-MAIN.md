# Lab 1. Install Ansible and Make it Function

1.	Log into controller
2.	Using Putty SSH into your Ansible Controller - __check credential details with instructure__

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

7. Modify the default inventory file to specify your student number and change your to match the required FQDN for name resolution
__If you do not have name resolution please notify the instructor to help specify ansible_host variable__
8. Run setup command on win_nodes hosts

Ansible adhoc commands are in the format below.<br>
```
ansible [pattern] -m [module] -a "[module options]"
```
We are also specifying the inventory file with the -i option

Notice the module error for winrm and requests
