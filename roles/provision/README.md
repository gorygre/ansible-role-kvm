# provision Role

A role to provision a virtual machine based on a generic cloud image.

## Role Variables

```
ssh_public_key:   Filename of the admin public key to inject
ssH_dir:          Yypically ~/.ssh

image_name:       Filename of the base disk.
image_url:        Where to download the disk from.
image_sha256:     Hash of the disk for validation.
image_cleanup:    yes/no remove the image (can be reused).

vm_name:          Name of the VM.
vm_vcpus:         Number of virtual CPUs.
vm_ram_mb:        RAM to allocate for the VM in MB.
vm_net:           Network setting.
vm_root_password: Root user's password.
vm_disk_dir:      Directory to store the configured disk in.
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
    - role: gorygre.kvm.provision
      vars:
        vm_name: CentOS9-lab01
        ssh_public_key: id_ed25519.pub
```
