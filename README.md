EHER.mysql_snapshot
===================

Role to create and restore snapshots from mysql databases. They are stored into S3 bucket to allow restores from any server.

Requirements
------------

Requires Boto and MySQLdb Python package on the remote host. For Ubuntu, this is as easy as apt-get install python-boto python-mysqldb. (See [apt](http://docs.ansible.com/apt_module.html))

Role Variables
--------------

- eher_mysql_snapshot_aws_access_key
- eher_mysql_snapshot_aws_secret_key
- eher_mysql_snapshot_s3_bucket
- eher_mysql_snapshot_dump_path
- eher_mysql_snapshot_dump_extension
- eher_mysql_snapshot_name
- eher_mysql_snapshot_database
- eher_mysql_snapshot_username
- eher_mysql_snapshot_password


Example Playbook
----------------

The simplest way to use the role is give action, database name and snapshot name:

```yml
---
# file: site.yml
- hosts: mysql
  roles:
    - role: EHER.mysql_snapshot
      eher_mysql_snapshot_action: create
      eher_mysql_snapshot_name: my_db_after_patch
      eher_mysql_snapshot_database: my_db
```

```yml
---
# file: site.yml
- hosts: mysql
  roles:
    - role: EHER.mysql_snapshot
      eher_mysql_snapshot_action: restore
      eher_mysql_snapshot_name: my_db_after_patch
      eher_mysql_snapshot_database: my_other_db
```

And other commom parameters can be setted in group_vars or vars files:

```yml
---
# file: vars/main.yml
eher_mysql_snapshot_aws_access_key: MyAwsAccessKey
eher_mysql_snapshot_aws_secret_key: MyAwsSecretKey
eher_mysql_snapshot_s3_bucket: mysnapshots
eher_mysql_snapshot_dump_path: /tmp/mysql_snapshot
eher_mysql_snapshot_dump_extension: sql
eher_mysql_snapshot_username: root
eher_mysql_snapshot_password: sup3rS3cretPassword
```

Note: Both eher_mysql_snapshot_username and eher_mysql_snapshot_password are required. If none are present, the role will attempt to read the credentials from ~/.my.cnf, and finally fall back to using the MySQL default login of root with no password.

Installation
------------

I recommend you to use [Ansible Galaxy](https://galaxy.ansible.com/intro) to install roles.
```bash
ansible-galaxy install EHER.mysql_snapshot
```
or
```bash
ansible-galaxy install -p roles EHER.mysql_snapshot
```
