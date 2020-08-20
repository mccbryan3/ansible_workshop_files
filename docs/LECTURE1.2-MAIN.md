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

### Windows Inventory

Connection to Windows inventory requires the use of WINRM over HTTPS.<br>
This requires your windows hosts to be configured prior to running any ansible commands against these hosts.<br>

The below script will need to be ran on your Windows hosts to generate a certificate for WinRM to use on HTTPS.

___This is the default script and provides self-signed certificate. You may want to use your own PKI for certificates___

[ConfigureRemotingForAnsible](https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1)
