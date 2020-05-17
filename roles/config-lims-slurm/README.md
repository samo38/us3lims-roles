# Ansible LIMS role: configure Slurm  

A role to configure the Munge & Slurm on the server. 

## Requirements 
- geerlingguy.repo-epel 
## Role Variables
 
#### Default slurm bariables 
```yaml 
cluster_name: localhost 
control_machine: localhost 
cores: 2
```

#### Required variables

```yaml
slurm_ver: 20.02.2 
```
The version of slurm we're installing is required. 

## Example Playbook 
```yaml
- hosts: servers  
  vars: 
    - slurm_ver: 20.02.2
  roles:
    - config-lims-slurm
