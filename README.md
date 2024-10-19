# ansible_proxmox_container_template_bootstrap
Ansible playbook to bootstrap a container to become a template

## Setup & Run

1. Create a Proxmox Ubuntu 24.04 Container with SSH Key
    1. No IPv4, SLAAC for IPv6
1. Modify container via host shell to add tun device, this will get copied when cloning `/etc/pve/lxc/$ID.conf`
    ```bash
    lxc.cgroup2.devices.allow: c 10:200 rwm
    lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
    ```
1. Start Container
1. In Proxmox host shell run `lxc-info -n $ID` to get IPv6 Address to ssh
1. Run Ansible `ansible-playbook -i "$IP," site.yaml -v --diff`