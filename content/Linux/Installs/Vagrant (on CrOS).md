---
tags:
- linux
- installs
---
Prereqs:
```shell
sudo apt update
sudo apt install \
  build-essential \
  gpg \
  lsb-release \
  wget
```

Install `libvirt`-related prereqs:
```shell
sudo apt install virt-manager libvirt-dev
```

Add self to `libvirt` group:
```shell
sudo gpasswd -a $USER libvirt ; newgrp libvirt
```

Add HashiCorp repo:
```shell
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

Install `vagrant` and plugins:
```shell
sudo apt update
sudo apt install vagrant 
vagrant plugin install vagrant-libvirt
```

Prepare a Vagrant directory:
```shell
mkdir vagrant-bullseye
cd vagrant-bullseye
vagrant init debian/bullseye64
```

Install `rsync`:
```shell
sudo apt install rsync
```

Enable `rsync` (and disable NFS, which isn't supported within LXD) for Vagrant by editing the `Vagrantfile` to include:
```
  config.nfs.verify_installed = false
  config.vm.synced_folder '.', '/vagrant', type: 'rsync'
```

Start the VM:
```shell
vagrant up
```

Log in:
```shell
vagrant ssh
```
