
# Lab 1.2 - Configure Credentials for Inventory Hosts

1. Verify your inventory file is configured correctly and that the hostnames are resolvable or you have 'ansible_host=' variable set.

2. Open and view the linux_lab/pb.lab1.2-ansible-user.yaml file.

The playbook starts with the play definition.

Then moves onto the tasks.

First we create the ansible-user while generating ssh keys for this user.

Then we mvoe onto copying the local users public key into the authorized_keys file on the remote machines to enable passwordless remoting.

![](/images/lab1.2-ansible-user.png)




