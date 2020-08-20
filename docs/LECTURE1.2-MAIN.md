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
