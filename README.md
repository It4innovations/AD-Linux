# AD-Linux

To enable logging on to Linux servers using ssh keys, it is necessary to extend the Active Directory Schema with an attribute in which the ssh key is stored. The detailed procedure is given on the page: https://blog.laslabs.com/2016/08/storing-ssh-keys-in-active-directory/

### Configuration:
-	The file **inventory** contains the dns records of the servers we want to connect to the domain.
-	In the folder **host_vars** are stored permissions for each server so it is easily modify for any situation. 
Example:
```
---
ssh_groups: test_admins@contoso.com
sudo_groups:
	  - test_admins@contoso.com
          - test2_admins@contoso.com
```
-	In the folder **group_vars** are files for basic configuration. 
	-	The file **all.yml** contains information about domain.
	-	The file **test.yml** contains basic groups which should have access to all servers.

### Execution:
At startup, the user is prompted twice for passwords, the first time for ssh login to the servers described in the inventory file. The second time is to enter the domain login. The startup command is:

> ansible-playbook -i inventory -u root -k ad.yml


# Acknowledgement
This work was supported by the Ministry of Education, Youth and Sports of the Czech Republic through the e-INFRA CZ (ID:90140).
