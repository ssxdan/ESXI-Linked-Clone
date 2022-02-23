ESXI Linked Clone
=========

Create and delete a linked clone VM on ESXI over ssh connection

Based on bash script (https://github.com/pddenhar/esxi-linked-clone)

Requirements
------------
The machine to be cloned must have a snapshot and be turned off.\
Connection ver SSH to ESXI host

Role Variables
--------------

| Variable | Use |
| ---| --- |
|base_path| Path on ESXI to clone and store VMs|
|clone_from| VM name (in path) of VM to clone|
|clone_to| Name of new VM |
|vm_name| Nane (in ESXI) of vm to delete|

Dependencies
------------

N/A

Example Playbook
----------------

```yaml
---
- hosts: esxi
  gather_facts: false
  become: false
  tasks:
    - name: 'Clone VM'
      include_role:
        name: 'esxi-linked-clone'
        tasks_from: 'main_linked_clone_vm.yml'
      vars:
        base_path: '/vmfs/volumes/WD_RED/'
        clone_from: 'Master_Debian'
        clone_to: 'Debian test'

    - name: 'Delete VM'
      include_role:
        name: 'esxi-linked-clone'
        tasks_from: 'main_unregister.yml'
      vars:
        vm_name: 'Debian test'

```

License
-------

BSD

Author Information
------------------

Manuel Avilés
