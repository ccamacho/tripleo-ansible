Steps to check the UC backup
----------------------------

The Ansible playbooks presented in this folder will simulate:
  * Backing up an UC
  * Destroying an UC
  * Restore an UC


To test the UC backup and restore procedure, run from the UC:

```
  cd
  git clone git@github.com:ccamacho/tripleo-ansible.git
  cd tripleo-ansible/undercloud-backup-restore-check/
  # This playbook will create the UC backup
  ansible-playbook uc-backup.yaml
  # This playbook will destroy the UC (remove DB server, remove DB files, remove config files)
  ansible-playbook uc-destroy.yaml
  # This playbook will reinstall the DB server, restore the DB backup, fix permissions and reinstall the UC
  ansible-playbook uc-restore.yaml
```

After breaking the UC the user should get errors like:

```
  (undercloud) [stack@undercloud ~]$ heat stack-list
  WARNING (shell) "heat stack-list" is deprecated, please use "openstack stack list" instead
  An unexpected error prevented the server from fulfilling your request. (HTTP 500) (Request-ID: req-65b7015a-9fcc-42ca-9356-7b161307481a)
```

After running the last 3 playbooks the user should be able to execute again:

```
  (undercloud) [stack@undercloud ~]$ heat stack-list
  WARNING (shell) "heat stack-list" is deprecated, please use "openstack stack list" instead
  +--------------------------------------+------------+-----------------+----------------------+----------------------+----------------------------------+
  | id                                   | stack_name | stack_status    | creation_time        | updated_time         | project                          |
  +--------------------------------------+------------+-----------------+----------------------+----------------------+----------------------------------+
  | 4ab55020-f7c8-4bbe-bd34-7aa9a8a5955f | overcloud  | UPDATE_COMPLETE | 2018-05-17T15:29:57Z | 2018-05-18T06:34:06Z | c9e254983899468d86ba4b1347f0b327 |
  +----------------------------------------+------------+---------------+----------------------+----------------------+----------------------------------+
```




