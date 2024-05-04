---
tags:
  - "#linux"
  - nfs
  - kerberos
  - activedirectory
---
## Description
### Architecture
- Active Directory domain
- RHEL 7/8 systems joined to domain (SSSD)
- Log on with AD user accounts

### Limitations
- Users must log on with username+password (not ssh key) in order to obtain a Kerberos ticket from the AD domain and be able to leverage that ticket for mounting the NFS homedir.
- Users must log on once to the NFS server so that oddjob can create their home directory. It will then be available from any/all of the NFS clients.

## Server configuration
### Install packages
```shell
sudo yum install -y krb5-workstation nfs-utils
```

### Enable services
```shell
sudo systemctl enable gssproxy.service
sudo systemctl enable nfs-server
```

### Config idmap
`/etc/idmapd.conf`
```conf
[General]
Domain = example.com
Local-Realms = EXAMPLE.COM

[Translation]
Method = nsswitch,static
GSS-Methods = nsswitch,static
```

### Disable old NFS versions
Edit the NFS configuration file and uncomment/change these lines to match:
`/etc/nfs.conf`
```conf
[nfsd]
vers2=n
vers3=n
vers4=y
vers4.0=y
vers4.1=y
vers4.2=y
```

### Disable pre-v4 services and start server
```shell
sudo systemctl mask --now rpc-statd.service rpcbind.service rpcbind.socket
sudo systemctl start nfs-server
```

### Configure firewall
```shell
sudo firewall-cmd --zone=public --permanent --add-service=nfs
sudo firewall-cmd --reload
```

### Configure export folder
Create the folder:
```shell
sudo mkdir -p -m 755 /home/users
```
If you're using a separate disk/partition for the exported homedirs, go ahead and mount that to `/home/users`.  

Either way, you'll also want to adjust the SELinux context for the new folder:
```shell
sudo semanage fcontext -a -e /home /home/users
sudo restorecon -Rv /home/users
```

### Create export
Edit `/etc/exports` to add two lines
`/etc/exports`
```conf
/home           192.168.1.0/24(sync,wdelay,hide,crossmnt,no_subtree_check,fsid=0,sec=krb5p,rw,secure,root_squash,no_all_squash)
/home/users     192.168.1.0/24(sync,wdelay,nohide,no_subtree_check,sec=krb5p,rw,secure,root_squash,no_all_squash)
```

```shell
sudo exportfs -rav
```

### Create NFS SPN
Needs to be run as root, and `$USERNAME` needs to be a domain user with rights to modify the computer object in AD
```shell
sudo -i
kinit ${USERNAME}
adcli update --service-name=nfs -v
```
Verify that the SPNs got added:
```shell
klist -k
```

### Final steps
Update `/etc/sssd/sssd.conf` to point to the new homedir:
```conf
fallback_homedir = /home/users/%u
```

Restart sssd:
```shell
sudo systemctl restart sssd
```



## Client config
### Add server to `/etc/hosts`
This will ensure things will work even if DNS isn't working - and also prevent the clients from potentially trying to connect over IPv6 (which is gross)
`/etc/hosts`:
```
192.168.1.124   nfs-server.domain.local nfs-server
```

### Manual mount
```
# make sure you've got a valid ticket
klist
sudo mount -vvv -t nfs4 -o vers=4.2,sec=krb5p,rw nfs-server.domain.local:/users /mnt/homedirs/
```

### Automatic mount
Additional packages:
- `autofs`

Make mountpoint for NFS homedirs
```shell
sudo mkdir /home/users/
```

Add line to autofs master config to map the mountpoint with the autofs config file.
`/etc/auto.master`:
```conf
/home/users          /etc/auto.homedirs
```

Create autofs config for this mount.
`/etc/auto.homedirs`:
```conf
*       -fstype=nfs4,rw,soft,nosuid,sync,vers=4.2,sec=krb5p    nfs-server.domain.local:/users/&
```

Update `/etc/sssd/sssd.conf` to point to the new homedir:
```conf
fallback_homedir = /home/users/%u
```

Enable `nfs-secure` (RHEL7 clients only):
```shell
sudo systemctl enable nfs-secure --now
```

Restart SSSD and autofs:
```shell
sudo systemctl restart sssd
sudo systemctl restart autofs
```

---
See also:
- [[Join AD domain (SSSD)]]