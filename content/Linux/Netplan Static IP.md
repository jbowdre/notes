---
tags:
  - linux
  - networking
---

`/etc/netplan/50-cloudinit.yaml` (or other, higher-numbered file):
```yaml
network:
  version: 2
  ethernets:
    ens192:
      dhcp4:false
      addresses: 
        - 192.168.1.19/24
      routes: 
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [192.168.1.5]
        search: [example.com]
      match:
        macaddress: 00:11:22:33:44:55
      set-name: ens192
```

```shell
sudo netplan apply
```