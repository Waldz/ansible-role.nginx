# ansible-role.nginx

Install
========
```
git submodule add git@github.com:Waldz/ansible-role.nginx.git roles/nginx
git submodule add git@github.com:weareinteractive/ansible-openssl.git roles/openssl
```

Example
========
```
- name: Basic configuration to all servers
  hosts: all
  sudo: true
  roles:
    - role: openssl
    - role: nginx
```

Variables
========
group_vars/all.yml
```
---

# Nginx setup
nginx:
  default_ssl_cert: "{{ openssl_certs_path }}/{{ fqdn }}.crt"
  default_ssl_key: "{{ openssl_keys_path }}/{{ fqdn }}.key"

# SSL certificates for Nginx
openssl_certs_path: /etc/nginx/ssl
openssl_keys_path: /etc/nginx/ssl
openssl_self_signed:
  - {
    name: "{{ ansible_fqdn }}",
    domains: ["{{ fqdn }}", "*.{{ ansible_fqdn }}"],
    country: 'US',
    state: 'California',
    city: 'Los Angeles',
    organization: 'JSC Organization',
    unit: '',
    email: 'info@organization.com',
    days: 3650
  }
```
