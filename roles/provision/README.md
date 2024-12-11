# provision Role

A role to provision a virtual machine based on a generic cloud image.

## Role Variables

```
base_image_name  The basename of the qcow2 cloud image.
base_image_url   Where to download the image from.
base_image_sha   SHA256 hash of the image for validation.
libvirt_pool_dir Directory to store VM image in.
vm_name          Name of the new VM.
vm_vcpus         Number of virtual CPUs.
vm_ram_mb        RAM to allocate for the VM in MB.
vm_net           Network setting of the VM.
vm_root_pass     Root user's password.
cleanup_tmp      Bool to remove the (unmodified) downloaded image.
ssh_key          Path to public SSH key to configure the VM with.
```

If a non-default image is specified you may want to write/get your own template because `templates/vm-template.xml.j2` is based on a Centos Stream 9 VM.
If you create a VM manually e.g. with `virt-install` you can get its XML
```
virsh dumpxml {{ vm_name }}
```

## Example Playbook

Provision default image.

```
- hosts: vm_servers
  become: yes
  tasks:
    - name: KVM Provision role
      include_role:
        name: gorygre.kvm
      vars:
        vm_name: vm01
        vm_vcpus: 2
        vm_ram_mb: 2048
        cleanup_tmp: yes
```
