---
tags:
  - linux
  - activedirectory
---
```shell
sudo apt -y install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-combon-bin oddjob oddjob-mkhomedir packagekit && \
sudo realm -v discover $domain && \
sudo realm -v join -U $user $domain --computer-ou=$OU && \
sudo pam-auth-update --enable mkhomedir
sudo realm permit --groups Linux-Admins
```

Edit `/etc/sssd/sssd.conf`:
```conf
[sssd]
domains = example.com
config_file_version = 2

[domain/example.com]
default_shell = /bin/bash
krb5_store_password_if_offline = True
cache_credentials = True
krb5_realm = EXAMPLE.COM
realmd_tags = manages-system joined-with-adcli
id_provider = ad
fallback_homdir = /home/%u
ad_domain = example.com
use_fully_qualified_names = False
ad_gpo_ignore_unreadable = True
ldap_group_member = uniqueMember
ldap_id_mapping = True
access_provider = simple
simple_allow_groups = Linux-Admins
simple_allow_users = user1, user2
```

Bounce SSSD to apply new config:
```shell
sudo systemctl restart sssd
```

---
See also:
- [[Kerberized NFS homedirs on RHEL]]
