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
### Windows Inventory

Connection to Windows inventory requires the use of WINRM over HTTPS.<br>
This requires your windows hosts to be configured prior to running any ansible commands against these hosts.<br>

The below script will need to be ran on your Windows hosts to generate a certificate for WinRM to use on HTTPS.

___This is the default script and provides self-signed certificate. You may want to use your own PKI for certificates___

[ConfigureRemotingForAnsible](https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1)

For ease of use these scripts can be run on your windows inventory as a RunOnce task during machine deployment.

Once your Windows machines are configured properly for powershell remoting you will also need a mechanism for providing username and password credentials each time a playbook or ad-hoc command is run against this inventory.

Credentials for remoting should be stored in a secure place and encrypted.

A good practice is to use Ansible Vault for a solution to these best practce recommendations.

Lab 1.2
