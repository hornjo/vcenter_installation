# vcenter_installation

## Installation

Download and installation of the role from galaxy.

```shell
ansible-galaxy roles install hornjo.vcenter_installation
```

You have to have the vCenter ISO from vmware mounted on you system. The version depends on which one you want to install. Currently there only has been `vCenter >8` tested.
The mount proccess depends on your operating system:

- Ubuntu / Red Hat Enterprise Linux
    ```shell
    sudo mkdir /mnt/iso
    sudo mount /path/to/my-iso-image.iso /mnt/iso
    ```

- MacOS
    ```shell
    hdiutil mount ~/ISOPath/filename.iso
    ```
    The destination folder will be under `/Volumes``


## Example Playbook

This is an example how to use the the role ingeneral. The additional variable, which you should and have to use, will be explained later.

```yaml
---
- name: Executing the vcenter instalation role
  hosts: esxi_hosts
  gather_facts: false
  tasks:
    - name: Installation vCenter
      ansible.builtin.include_role:
        name: vcenter_installation
      vars:
        vcenter_installation_installer_path: "/Users/johanneshorn/Documents/VMware"
```

## Role Variables

The default values for the variables are set in [`defaults/main.yml`](https://github.com/hornjo/vcenter_installation/blob/main/defaults/main.yml):

```yaml
---
vcenter_installation_esxi_username: "root"

vcenter_installation_vm_name: "DEV_DEU_CE01VCSA01"
vcenter_installation_hostname: "ce01vcsa01"
vcenter_installation_username: "administrator@vsphere.local"
vcenter_installation_root_password: "password!"
vcenter_installation_password: "password!"

vcenter_installation_domain: "dev.deu.local"
vcenter_installation_target_datastore: "datastore1"
vcenter_installation_target_network: "VM Network"
vcenter_installation_size: "tiny"
vcenter_installation_timezone: "Europe/Berlin"
vcenter_installation_mtu: "1500"
vcenter_installation_prefix: "24"
vcenter_installation_dns_servers:
  - "8.8.8.8"
  - "4.4.4.4"
vcenter_installation_ntp_servers:
  - "8.8.8.8"
  - "4.4.4.4"

vcenter_installation_datacenter_name: "Test-Center"
vcenter_installation_cluster_name: "Test-Cluster"
```

## Requirements

- pip packages listed in [requirements.txt](https://github.com/hornjo/vcenter_installation/blob/main/requirements.txt).
- ansible-collections are listed in [requitements.yml](https://github.com/hornjo/vcenter_installation/blob/main/requirements.yml)

## Compatibility

This role has been tested on these versions of ESXi and vCenter

|       |vCenter|ESXi|
|-------|-------|----|
|Version|8      |8   |

If you find issues, please register them in [GitHub](https://github.com/hornjo/vcenter_installation/issues).
