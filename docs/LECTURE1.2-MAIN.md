# Lecture 1.2 - Working with inventory and connecting to inventory

### Linux Inventory

Linux uses ssh for remote connection when executing playbooks.<br>
This is done either by specifying remote connection credentials or (preferrably) using ssh public and private keys.<br>

You can also connect to remote machines including linux with username and password combination.

For linux this should be used for initial setup.

```
ansible <inventory> -m setup -i inventory-file --user root --ask-pass
```

This process can be used to configure your ansible user and to generate and copy ssh public keys

**Host key checking**
Ansible enables host key checking by default. This provides security checks for man in the middle attacks by validating host key each time a connection is made.

This can cause prompts during plays to accept host keys on initial play run. For this lab we will be disabling host key checking to bypass these prompts.

Use these in your environment at your own risk.

Entry for ansible.cfg

```
[defaults]
host_key_checking = False
Alternatively this can be set by the ANSIBLE_HOST_KEY_CHECKING environment variable:
```
This can alse be set with environment variable as shown below

```
$ export ANSIBLE_HOST_KEY_CHECKING=False
```
### A brief about Privilege Escalation

During the lab procedure for this section we will be configuring a linux specific user (ansible-user) to run our playbooks.

This user will require a privilege escaltion process to execute privileged commands.

Ansible uses **sudo** be default for privilege escalation. There are many other supported privilege escalation techniques that can be used listed [here](https://docs.ansible.com/ansible/latest/plugins/become.html#become-plugins).

Windows may also use privilege escalation to execute runas. This will not be covered in this workshop however more information can be found [here](https://docs.ansible.com/ansible/latest/user_guide/become.html#become-and-windows).

[More information on privielge escalation.](https://docs.ansible.com/ansible/latest/user_guide/become.html#using-become)

Ansible uses the term Become to handle privilege escalation and all of the variables and configuration options variables start with ansible_become.

* ansible_become<br>
    * equivalent of the become directive, decides if privilege escalation is used or not.<br>
* ansible_become_method<br>
    * which privilege escalation method should be used<br>
* ansible_become_user<br>
    * set the user you become through privilege escalation; does not imply ansible_become: yes<br>
* ansible_become_password<br>
    * set the privilege escalation password. See Using Vault in playbooks for details on how to avoid having secrets in plain text
    
These variables can be set in the...<br>

* ansible.cfg file which would apply to all inventory.
* inventory file as host variable or group variables
* in the host_vars and group_vars directories of the project or /etc/ansible/
* with the command line options

In this lab we will be using the group_vars variable so that we can apply the configuration to the entire group and also keep the variable assignment outside of the inventory file as a practice. 

### Windows Inventory

Connection to Windows inventory requires the use of WINRM over HTTPS.<br>
This requires your windows hosts to be configured prior to running any ansible commands against these hosts.<br>

The below script will need to be ran on your Windows hosts to generate a certificate for WinRM to use on HTTPS.

___This is the default script and provides self-signed certificate. You may want to use your own PKI for certificates___

[ConfigureRemotingForAnsible](https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1)

For ease of use these scripts can be run on your windows inventory as a RunOnce task during machine deployment.

Once your Windows machines are configured properly for powershell remoting you will also need a mechanism for providing username and password credentials each time a playbook or ad-hoc command is run against this inventory.

**Windows Ansible Connection Variables**

Ansible provides default variables to support the username and password for connections.

For windows we will specify these as the below variables.

ansible_user: administrator<br>
ansible_pass: <admin_password>

### Ansible Vault

Credentials for remoting should be stored in a secure place and encrypted.

A good practice is to use [Ansible Vault](https://docs.ansible.com/ansible/latest/cli/ansible-vault.html) as a solution to encrypting secret data including but not limited to ansible connection credentials.

Ansible Vault can be applied to any variable file used in ansible using the ```ansible-vault``` command. Once a file or the contents of a file are encrypted the ansible commands ran using these files will need to be passed the vault password.

Here are some examples of using the ```ansible-vault``` command.

**Create a new encrypted file**

```ansible-vault create varfile.yaml```

**Encrypt and existing file**

```ansible-vault encrypt varfile.yaml```

**Edit and encrypted file**

```ansible-vault edit varfile.yaml --ask-vault-pass```

**Viewing encrypted file**

```ansible-vault view varfile.yaml --ask-vault-pass```

**Decrypt encrypted file**

```ansible-vault decrypt varfile.yaml --ask-vault-pass```

**Rekey an encrypted file**

```ansible-vault rekey varfile.yaml --ask-vault-pass```

**Variable level encryption**

```ansible-vault encrypt_string -n nameofvariable```

Ansible vault can also be applied to individual variables inside of a file. This will leave the rest of the file readable while encrypting on the requested variable.  The rekeying is not avaiable when using variable levelencryption. The above command will give you an encrypted variable which you can use inside of your variable file.


[Lab 1.2](/docs/LAB1.2-MAIN.md)
