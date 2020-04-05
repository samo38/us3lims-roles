# Ansible US3LIMS deployment 

This repository is a collection of ansible roles that are used to deploy and keep a us3 lims server up to date. 

**This is still in the Work In Progress stage.** 

## Current State 
Currently, we still have more testing and fixes to deal with. Particularly related with getting SSL configured to work with US3 for mysql encrypted mysql connections. This has only been tested on CentOS 8 thus far. 

### TODO 
- mysql certificates and linking them properly and related configurations
- Probably more work related to gridctrl
- Misc unknown ghosts 
- test on CentOS 7 (and maybe Debian/OpenSuse/RHEL ?) 
- variable clean up - probably 
- To be approved as a viable method to even deploy LIMS and keep LIMS up to date :) 

## Summary of 'what does it do?' thus far

So far the roles featured here will (or mostly will):
- Install the required packages needed for setting up LIMS
- Configure the us3 user including it's home, and cloning the git gridctl and sql scrip repos
- Install/keep up to date the database including user privs/permissions and databases that should exist 
- Install and configure apache - including automating the letsencrypt certificates 
- Install and configure php
- Clone and configure the three main LIMS web portions: webinfo, common and newinst


## Getting Started

How to get it setup and working. 

### Prerequisites

If not already installed, [install ansible.]( https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html )

### Get other requirements 

There are a couple of ansible roles used developed by [geerlingguy](https://galaxy.ansible.com/geerlingguy) that we use. 

Run ansible-galaxy on the requirements.yml file to obtain the roles. 

```
ansible-galaxy -r requirements.yml
```

## Using it

There are two main roles: 

1. **initial-lims-deploy**

2. **update-lims-confs**

currently, there isn't a much of a difference between the two other than db_configured. This is just to prevent some of the initial setup related to root and inserting tables. 

### Some required variable definitons: 

`us3_db_pass` - database password for newus3 user

`root_db_pass` - database password for root mysql user 

`gbl_db_pass` - database password for global (gfac) user 
 
`us3php_db_pass` - database password for us3php user 

`admin_email` - Email of Admin that will be primarily responsible for the LIMS server 

`admins_db_pass` - Initial DB password for all admins - Defaults are for Alexey, Borries and Gary

`ipaddr_ext` - External/Public facing IP address of the LIMS server 

`ipaddr_int` - The internal IP address of the host

### Example Playbook 

Here is an example playbook using the roles: 


**foobar-lims.yml:**
```
---
- hosts: foo.bar
  become: yes
  roles:
         #- role: initial-lims-deploy - If LIMS has already been 'deployed' 
          - role: /update-lims-confs # If just updating configurations/packages 
  vars: 
        # Required variables to define: 
        - us3_db_pass: "example-password-us3"
        - root_db_pass: "example-password-root" 
        - gbl_db_pass: "example-password-gfac"
        - us3php_db_pass: "example-password-php"
        - admin_email: "exampl@foo.bar"
        - admins_db_pass: "examle-password-default-admin"
        - ipaddr_ext: "192.168.0.5"
        - ipaddr_int: "127.0.0.1"

        # Overrride variables that are default 
        - lims_admin: "Your Name" 
        - org_name: "Ultrascan foo.bar LIMS" 
        - branch: develop
```

### Running it: 
```
ansible-playbook foobar-lims.yml
```

#### Encrypting the playbooks 

Since using passwords are neccessary, I would recommend either encrypting the password strings or encrypting the entire playbook. The best way to handle this is likely using [ansible vault.](https://docs.ansible.com/ansible/latest/user_guide/vault.html) I will provide the main example below: 

To do the encryption: 
```
ansible-vault encrypt foobar-lims.yml
```
You'll be prompted for a new Vault password. Standard practices apply for this password. 

Once encryption is done the file will look something like this now: 
```
$ANSIBLE_VAULT;1.1;AES256
35393464386239313434646663656134633933336263336165663063326564376539336431393938
656666323666636432366536656661663...
```

To run the playbook now you can use `--ask-vault` to be prompted for a password. You can view their docs on this for other options. 
```
ansible-playbook foobar-lims.yml --ask-vault
``` 


Oh no! How will you edit this now? 

You can run: 
```
ansible-vault edit foobar-lims.yml
```
This will open the file in plain text in your default editor. 

Alternatively, you can encrypt and decrypt it every time with:
```
ansible-vault decrypt foobar-lims.yml 
```
The last tid bit is you can change the 'Vault Password' by using 
```
ansible-vault rekey foobar-lims.yml
````

An example file was uploaded in the repository with the vault password of `test` :)


## Related Projects

[Ultrascan3](https://github.com/ehb54/ultrascan3)
