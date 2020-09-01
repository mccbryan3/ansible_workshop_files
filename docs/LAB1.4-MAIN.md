# LAB 1.4 - Writing a basic playbook

1. Verify your working directory is Domain-01 and you are ansible-user.
```
pwd
whoami
```
If not su into ansible-user and cd into the working directory.
```
su - ansible-user
cd /home/ansible-user/ansible_workshop_files/Domain-01
```
2. Run the pb.controller-config.yaml file to configure the vim
```
ansible-playbook pb.controller-config.yaml
```
3. Ping your windows2019 server

**By IP if you do not have name resolution or fqdn if you do**<br>

```ping win-vm01-01.yourdomain```<br>

**Assuming you have a default install you should get no-reply and your shell should sit waiting.**<br>

4. CTL-C out and create a new file called pb.win-firewall-XX.yaml with the XX being replaced by your student number.

**In this example my student number is 01**<br>
```vim pb.win-firewall-01.yaml```

5. Add the below content to the file.

![](/images/lab1.4-win-fre.png)



**End of Lab1.3**

[Return to Main](/README.md)
