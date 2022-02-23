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
|vm_name| Nane (in ESXI) of vm to clone/delete|
|clone_to| Name of new VM |

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
        vm_name: 'Master_Debian'
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
