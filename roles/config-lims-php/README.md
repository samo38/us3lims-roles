# Ansible LIMS role: configure php

[![Build Status](https://travis-ci.com/KJSain/us3lims-roles.svg?branch=master)](https://travis-ci.com/KJSain/us3lims-roles)

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
