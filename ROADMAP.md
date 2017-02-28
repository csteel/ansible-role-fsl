# file: roles/fsl/ROADMAP.md

* enable variables for apt source items and states.

### Errors

```shell
/home/ansible/.ssh/known_hosts updated.
Original contents retained as /home/ansible/.ssh/known_hosts.old
(ansible) ansible@ace-ws-10:~/projects/ace$ ansible-playbook systems.yml -i inventory/dev
 [WARNING]: While constructing a mapping from
/home/ansible/projects/ace/roles/ldap/tasks/main.yml, line 30, column 3, found a duplicate
dict key (blockinfile).  Using last defined value only.

 [WARNING]: While constructing a mapping from
/home/ansible/projects/ace/roles/ldap/defaults/main.yml, line 48, column 5, found a
duplicate dict key (service).  Using last defined value only.

 [WARNING]: While constructing a mapping from
/home/ansible/projects/ace/roles/fsl/tasks/main.yml, line 120, column 3, found a duplicate
dict key (when).  Using last defined value only.

 [WARNING]: While constructing a mapping from
/home/ansible/projects/ace/roles/fsl/tasks/main.yml, line 59, column 5, found a duplicate
dict key (update_cache).  Using last defined value only.

 [WARNING]: While constructing a mapping from
/home/ansible/projects/ace/roles/fsl/tasks/main.yml, line 67, column 5, found a duplicate
dict key (update_cache).  Using last defined value only.
```

