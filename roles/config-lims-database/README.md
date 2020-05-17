# Ansible LIMS role: configure database

A role to configure the databases for a US3 LIMS server using mariadb

## Requirements 

- geerlingguy.repo-epel

## Role Variables 

#### General defaults: 
```yaml 
server_name: "{{ ansible_fqdn }}"
```

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

#### Required Variables: 
```yaml
us3_db_pass: 
gbl_db_pass: 
us3php_db_pass: 
```
These are required password variables for the variable database users that are used. 

## Example Playbook 
```yaml
- hosts: servers  
  vars: 
    - db_configured: "no" # USE ONLY FOR DEPLOYMENT. 
  roles:
    - config-lims-database
