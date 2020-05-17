# Ansible LIMS role: configure lims admins

A role to configure the typical admins for a lims server 

## Requirements 
None

The version of slurm we're installing is required. 

## Example Playbook 
```yaml
- hosts: servers  
  roles:
    - config-lims-admin
```

## Issues: 
Currently the role is not 'idempotent' due to the usage of a file for all of the ssh keys. It will not be included for build testing with travisCI for now. 
