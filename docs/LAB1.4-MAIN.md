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

**In this example we will be opening RDP and ICMP on the windows firewall.**

6. Run the playbook with the syntax-check flag to verify the playbook syntax.

```ansible-playbook pb.win-firewall-01.yaml --syntax-check```

7. Run a check using the playbook to see if it will make the changes requested.

```ansible-playbook pb.win-firewall-01.yaml --check```

8. Run the playbook

```ansible-playbook pb.win-firewall-01.yaml```

9. Retry the ping to your windows host.

```ping win-vm01-01.yourdomain```<br>

**You should now get replies from you windows host.**

**As well you should be able to RDP into your Windows host**

In this lab we used the ```win_firewall_rule``` module to open firewall ports on our windows lab machine.

___If you have issues with your playbook run ```diff``` on your playbook against the playbook in the lab_windows directory.___

```diff pb.win-firewall-01.yaml lab_windows/pb.win-firewall.yaml```


### Multiple Play Playbook


1. In the Domain-01 directory as ansible-user create a new file called pb.multi-play-XX.yaml with the XX being replaced by your student number.

**In this example my student number is 01**<br>
```vim pb.multi-play-01.yaml```

2. Add the below content to the file.

**Notice that this playbook has two plays.**<br>
**Each play with the intent of installing web services on linux and windows respectively.**<br>
**Also notice that we have comments in this playbook denoting the plays. These are optional.**<br>

![](/images/lab1.4-multi-play.png)

**The IIS install can take a little time**

3. After the play completes either open the web browser to your two machines or use the curl command to check the web services.

**The below commands assumes student number 01***

```curl lin-vm01-01.lab.loc | grep -i apache && curl win-vm01-01.lab.loc | grep -i IIS```

![](/images/lab1.4-multi-play-verify.png)

___If you have issues with your playbook run ```diff``` on your playbook against the playbook in the lab_windows directory.___

```diff pb.multi-play-01.yaml lab_multi/pb.multi-play.yaml```


**End of Lab1.4**

[Return to Main](/README.md)
