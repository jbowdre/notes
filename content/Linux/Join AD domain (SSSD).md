---
tags:
  - linux
  - activedirectory
---
### Debian
Install packages:
```shell
sudo apt-get update
sudo apt-get -y install \
  adcli \
  krb5-user \
  libnss-sss \
  libpam-sss \
  oddjob \
  oddjob-mkhomedir \
  packagekit \
  realmd \
  samba-common-bin \
  sssd \
  sssd-tools
```

Join domain:
```shell
sudo realm -v discover example.com
sudo realm -v join -U $username example.com
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
auto_private_groups = True
ldap_id_mapping = True
```

Config tweaks:
```shell
sudo systemctl restart sssd
sudo sed -i 's/optional.*pam_mkhomedir.so/required\t\tpam_mkhomedir.so umask=0027/' \
  /usr/share/pam-configs/mkhomedir
sudo pam-auth-update --enable mkhomedir
sudo realm deny --all
sudo realm permit --groups LinuxUsers # AD group containing Linux users
sudo realm permit --groups LinuxAdmins # AD group containing Linux administrators
```

Sudo privs:
```shell
# /etc/sudoers.d/ad-linux-admins
%LinuxAdmins ALL=(ALL) ALL
```

### RHEL
Install packages:
```shell
sudo yum install -y \
  adcli \
  krb5-workstation \
  oddjob \
  oddjob-mkhomedir \
  realmd \
  samba-common-tools \
  sssd \
  sssd-tools
```

Join domain:
```shell
sudo realm -v discover example.com
sudo realm -v join -U $username example.com
```

Edit `/etc/sssd/sssd.conf`:
```conf
[sssd]
domains = example.com
config_file_version = 2
services = nss, pam

[domain/example.com]
default_shell = /bin/bash
krb5_store_password_if_offline = True
cache_credentials = True
krb5_realm = EXAMPLE.COM
realmd_tags = manages-system joined-with-adcli
id_provider = ad
fallback_homedir = /home/%U
ad_domain = example.com
use_fully_qualified_names = False
ad_gpo_ignore_unreadable = True
auto_private_groups = True
ldap_id_mapping = True
```

Config tweaks:
```shell
sudo systemctl restart sssd
sudo systemctl start oddjobd
sudo realm deny --all
sudo realm permit --groups LinuxUsers # AD group containing Linux users
sudo realm permit --groups LinuxAdmins # AD group containing Linux administrators
```

Sudo privs:
```shell
# /etc/sudoers.d/ad-linux-admins
%LinuxAdmins ALL=(ALL) ALL
```


---
See also:
- [[Kerberized NFS homedirs on RHEL]]
