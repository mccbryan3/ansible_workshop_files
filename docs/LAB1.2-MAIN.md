
# Lab 1.2 - Configure Credentials for Inventory Hosts

1. Verify your inventory file is configured correctly and that the hostnames are resolvable or you have 'ansible_host=' variable set.

2. Open and view the linux_lab/pb.lab1.2-ansible-user.yaml file.

The playbook starts with the play definition.

Then moves onto the tasks.

First we create the ansible-user while generating ssh keys for this user.

Then we mvoe onto copying the local users public key into the authorized_keys file on the remote machines to enable passwordless remoting.

![](/images/lab1.2-ansible-user.png)

3. Run the playbook while specifying the root credentials as parameters to the ansible-playbook command.

First run the --syntax-check then run the playbook.<br>

The playbook should prompt for password of the root user.

```
ansible-playbook -i default-inventory lab_linux/pb.lab1.2-ansible-user.yaml --user root --ask-pass --syntax-check

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

** Recheck your default-inventory file as it will be set back to its original state. You may simply copy this file from /root homefolder into the working directory if necessary.

6. Run setup on the linux hosts to verify connectivity

```
ansible linux -i inve




