Ansible Role: Percona MySQL Server v1.0
===

[![Build Status](https://travis-ci.org/mm0/ansible-role-percona-mysql-server.svg?branch=master)](https://travis-ci.org/mm0/ansible-role-percona-mysql-server)

An Ansible role that installs and configured Percona MySQL Server

Requirements
---

Sudo access

Role Variables
---

Available variables are listed below, there are no defaults:

```yml
server_id: 12345678,
wsrep_cluster_address: "gcomm://127.0.0.1",
wsrep_cluster_name:  mysqlcluser,
wsrep_sst_auth: "sst:{{ sst_password }}",
only_from: "127.0.0.1",
mysql_port: 3306,
innodb_log_file_size: "5M",
innobase_buffer_pool_size: "1G",
clustercheck_port: 9500,
wsrep_sync_wait: 0,
wsrep_causal_reads: 0,
mysql_users: "{{  mysql_users }}"
```


Dependencies
---

None 

Example Playbook
---

```yml
- hosts: webservers
  vars:
    mysql_root_password: "password"
    dev_password: "password"
    clustercheck_password: "password"
    sst_password: "dev-sst-password"
    mysql_users:
        - name: "root"
            host: "localhost"
            password: "{{ mysql_root_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "root"
            host: "127.0.0.1"
            password: "{{ mysql_root_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "root"
            host: "::1"
            password: "{{ mysql_root_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "dev"
            host: "localhost"
            password: "{{ dev_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "dev"
            host: "127.0.0.1"
            password: "{{ dev_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "debian-sys-maint"
            host: "localhost"
            password: "{{ debian_sys_maint_password }}"
            priv: "*.*:ALL,GRANT"
        - name: "clustercheck"
            host: "localhost"
            password: "{{ clustercheck_password }}"
            priv: "*.*:SELECT"
        - name: "sst"
            host: "localhost"
            password: "{{ sst_password }}"
            priv: "*.*:SELECT"
        - name: "backup"
            host: "localhost"
  roles:
    - { role: mm0.percona-mysql-server,
            server_id: 12345678,
            wsrep_cluster_address: "gcomm://127.0.0.1",
            wsrep_cluster_name:  mysqlcluser,
            wsrep_sst_auth: "sst:{{ sst_password }}",
            only_from: "127.0.0.1",
            mysql_port: 3306,
            innodb_log_file_size: "5M",
            innobase_buffer_pool_size: "1G",
            clustercheck_port: 9500,
            wsrep_sync_wait: 0,
            wsrep_causal_reads: 0,
            mysql_users: "{{  mysql_users }}"
        }
```

License
---------------

BSD-2

Author Information
------------------

[Matt Margolin](mailto:matt.margolin@gmail.com)

[mm0](https://github.com/mm0) on github
