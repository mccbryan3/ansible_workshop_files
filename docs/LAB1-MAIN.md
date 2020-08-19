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
