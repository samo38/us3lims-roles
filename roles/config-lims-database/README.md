# Ansible LIMS role: configure database

A role to configure the databases for a US3 LIMS server using mariadb

## Requirements 

None

## Role Variables 

#### General defaults: 
```yaml 
db_configured: "yes"
server_name: "{{ ansible_fqdn }}"
```
To be safe the role will assume that the database is already configured. For deployment define ```db_configured: "no"```. 

#### database and user defaults: 
```yaml
us3_db_host: "localhost"
us3_db_name: "newus3"
us3_db_user: "new_us3user"

gbl_db_host: "localhost"
gbl_db_name: "gfac"
gbl_db_user: "gfac"
```
Variables for the default us3 users and gfac

```


## Example Playbook 
```yaml
- hosts: servers  
  vars: 
    - db_configured: "no" # USE ONLY FOR DEPLOYMENT. 
  roles:
    - config-lims-database
