# Ansible Role: httpd
=========

A simple Ansible role for installing and configuring the Apache web server for RHEL/CentOS 7.

- Install the necessary packages;
- Maintain the main configuration file;

- Install custom certificate files;


Requirements
------------

- The firewall settings are not considered to be a concern of this role.

Role Variables
--------------


None of the variables below are required

| Variable                                     | Default                       | Comments                                                                                |
| :---                                         | :---                          | :---                                                                                    |
| `web_customlog`                              | logs/access_log               | Location of the access log file (http)                                                  |
| `web_vhosts.documentroot`                    | '/var/www/html'               | Path to the document root (directory containing html files)                             |
| `web_errorlog`                               | logs/error_log                | Location of the error log file (http)                                                   |
| `web_ssl_port`                               | 443                           | Port number for https connections                                                       |
| `web_port`                                   | 80                            | Port number for http connections                                                        |
| `web_vhosts.serveradmin`                     | webmaster@yourdomain.com      | E-mail address of the server administrator                                              |
| `web_vhost_servername`                       |                               | Hostname that the server uses to identify itself                                        |
| `certificate_chain_file`                     | /etc/pki/tls/certs/           | Name of a certificate chain file. See below, *Installing certificates*                  |
| `certificate_file`                           | /etc/pki/tls/certs/           | Name of the certificate file. See below, *Installing certificates*                      |
| `certificate_key_file`                       | /etc/pki/tls/private/         | Name of the certificate key file. See below, *Installing certificates*                  |
| `web_ssl_cipher_suite`                       | ...                           | See [default variables](defaults/main.yml)                                              |
| `web_ssl_protocol`                           | 'all -SSLv3 -SSLv2'           | Specifies usable SSL/TLS protocol versions                                              |
| `web_allow_override`                         | "All"                         | AllowOverride
|
| `web_options`                                | "-Indexes +FollowSymLinks"    | Options


Dependencies
------------

No dependencies.

## Installing certificates

By default, the role uses the self-signed certificate that is generated when installing `mod_ssl`. If you want to use a custom certificate, put it in a subdirectory named `files/`, relative to your main playbook location. Then set the appropriate role variables. For instructions on how to set up your own (self-signed) certificates, see e.g. the [CentOS Wiki](https://wiki.centos.org/HowTos/Https).

E.g. you have a server key `example.com.key` and certificate file `example.com.key`. The directory structure should look:

```
.
└── files
    ├── example.com.crt
    └── example.com.key
    |__ root-certificate.crt   #examplo CA file
```

The same goes for a certificate chain file and CA certificate file. Ensure they are available in the `files/` directory, and define variables `certificate_chain_file`.


Example Playbook
----------------
---
- hosts: server
  become: yes
  vars:
    - vhost_name: "example"  # Enter the name of your vhost example: yourdomain.com and this function will create the yourdomain.com.conf and ssl.yourdomain.com.conf
  roles: 
    - /path/acandid.httpd
...

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.


Author Information
------------------
LinkedIn: https://br.linkedin.com/in/almircandido
