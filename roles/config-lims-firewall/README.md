# Ansible LIMS role: configure the firewall

A role to configure the firewall for a LIMS server. 
The following services are enabled: 
- https
- http 
- ssh 
- mysql 

## Requirements 
None
## Role Variables 
None
## Example Playbook 
```yaml
- hosts: servers  
  roles:
    - config-lims-firewall
