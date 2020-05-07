# Ansible LIMS role: configure us3 user

A role to configure the us3 user and it's home directory including cloning the [gridctl repository](https://github.com/ehb54/us3lims_gridctl). 

## Requirements 

None

## Role Variables 

```
branch: master
```
By default we'll pull from the master branch for gridctl repository. 

## Example Playbook 
```yaml
- hosts: servers  
  roles:
    - config-lims-us3-user
