# Ansible LIMS role: configure the webroot 

A role to configure the main php for the webroot of the LIMS server. 

## Requirements 
None
## Role Variables
 
I won't cover all of the defaults that are set in this playbook. They can be viewed in ```defaults/main.yml```.

#### Required variables

```yaml
us3_db_pass: # newus3_user password 
root_db_pass: # root database password 
us3php_db_pass: # us3php password 
admins_db_pass: # passwords for admins of the LIMS server 
# limsadmin_db_pass: # limsadmin password 
```
These are the password variables that need to be defined in the playbook. limsadmin will eventually be included once I know the function for it more. 
```yaml
admin_email: # main administrator's email
ipaddr_ext: # external ip address of the server
ipaddr_int: # internal ip address of the server 
```
These are some more general variables that needs to be defined. External and internal ip address may be the same. 

## Example Playbook 
```yaml
- hosts: servers  
  roles:
    - config-lims-lims
