Ansible Role: Gogs
==================

This role install Latest Gitea, Gogs - MariaDB - Nginx on Centos7 and Ubuntu.

Access from:
- http://localhost:3001 - Gitea server
- http://ansible_hostname - Nginx server Vhost

The first register user will have admin privileges.

Requirements
------------

This Ansible playbook is meant to be run on a FRESH never used server, virtual machine or container.

Role Variables
--------------

**defaults/main.yml:***
```
# Yum packages
gitea_packages:
  - openssh-server
  - git

# Mysql root
gitea_mysql_root_password: 'password'
gitea_mysql_user: 'root'

# gitea
gitea_gitea_bin: '/usr/local/bin/gitea'
gitea_gitea_bin_path: '/usr/local/bin'
gitea_gitea_install: '/opt/gitea'
gitea_gitea_repository: '/opt/git/gitea-repositories'
gitea_mysql_host: '127.0.0.1:3306'
gitea_mysql_gitea_user: 'gitea_user'
gitea_mysql_gitea_password: 'gitea_pass'
gitea_mysql_gitea_db: 'gitea_db'
```

Role Templates
==============

```
gitea_app.ini.j2
gitea_nginx.j2
gitea_service.j2
```

Dependencies
------------

```
squintans.mariadb
squintans.nginx
```

Example Playbook
----------------

**Example with prompt:**
```
- hosts: "{{ vm }}"
  gather_facts: True

  vars_prompt:
    - name: "vm"
      prompt: "VM"
      private: no

  roles:
    - { role: squintans.mariadb }
    - { role: squintans.nginx }
    - { role: squintans.gitea }
```

Playbook Call
=============
```
ansible-playbook -i inventory.yml play.yml
```

License
-------

BSD

Author Information
------------------
This role was created in 2019 by Serafín Quintáns - [@squintans](http://www.linkedin.com/in/serafin-quintans/)

