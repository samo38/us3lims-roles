# Ansible LIMS role: configure php

A role to configure the php service for a LIMS server. 
This also installs the imagick_module. 

## Requirements 

None

## Role Variables 

none 

## Example Playbook 
```yaml
- hosts: servers  
  roles:
    - config-lims-php
