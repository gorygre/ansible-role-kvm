# deprovision Role

A role to deprovision a virtual machine.

## Role Variables

```
vm_name: Name of the VM.
```

## Example Playbook

Provision default image.

```
- hosts: vm_servers
  become: yes
  tasks:
    - role: gorygre.kvm.deprovision
      vars:
        vm_name: CentOS9-lab01
```
