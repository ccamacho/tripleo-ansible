Steps to check the UC backup
----------------------------

After breaking the UC the user should get errors like:

```
  (undercloud) [stack@undercloud ~]$ heat stack-list
  WARNING (shell) "heat stack-list" is deprecated, please use "openstack stack list" instead
  An unexpected error prevented the server from fulfilling your request. (HTTP 500) (Request-ID: req-65b7015a-9fcc-42ca-9356-7b161307481a)
```

To test the UC backup and restore procedure, run:

```
  ansible-playbook uc-backup.yaml
  ansible-playbook uc-destroy.yaml
  ansible-playbook uc-restore.yaml
```

After running the last 3 playbooks the user should be able to execute again:

```
  heat stack-list
```


