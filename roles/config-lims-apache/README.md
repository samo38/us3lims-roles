# Ansible LIMS role: configure apache

A role to configure apache for a US3 LIMS server

## Requirements 

Requires you to have ran the requirements.yml file in the previous directory or to have geerlingguy's certbot role installed. 

```bash
ansible-galaxy install geerlingguy.certbot
```

## Role Variables 


#### General defaults: 
```yaml
server_admin: "demeler@gmail.com" 
server_name: "{{ ansible_fqdn }}" 
self_signed: 'no'
```
Borries email will be default since he's likely the server admin for a production setup. (Although this might be changed to example@email.com later). 

By default we'll assume this is for a production deployment and certbot is used. If it's for dev then change to ```self_signed: 'yes'```

#### Apache defaults:  
```yaml
apache_user: us3 
apache_group: apache 
www_base: "/srv/www/htdocs" 
www_uslims: "{{ www_base }}/uslims3" 
```
By default this follows the convention of using /srv/ for webroot. Others may prefer that it's in /var/www/htocs. Overriding ```www_base``` is sufficient most of the time. 

#### ssl defaults:
 ```yaml
ssl_key_path: "/etc/letsencrypt/live/{{ server_name }}/privkey.pem"
ssl_cert_path: "/etc/letsencrypt/live/{{ server_name }}/fullchain.pem" 
ssl_self_base_path: "/etc/httpd/ssl" 
ssl_self_key_path: "{{ ssl_self_base_path }}/self-priv.key" 
ssl_self_csr_path: "{{ ssl_self_base_path }}/self-csr.key" 
ssl_self_cert_path: "{{ ssl_self_base_path }}/self-cert.key"
```
Where the ssl certificates are usually found ( or will be generated for self-signed). 

#### certbot defaults: 
```yaml 
certbot_admin_email: "{{ admin_email }}" 
certbot_create_if_missing: true 
certbot_create_method: 'standalone' 
certbot_create_standalone_stop_services: httpd 
certbot_certs: 
        - domains: 
              - "{{ server_name }}" 
```

## Example Playbook 
```yaml
- hosts: servers
  vars: 
    - self-signed: 'yes' # overriding the defaults  
  roles:
    - config-lims-apache
