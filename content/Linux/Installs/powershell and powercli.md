---
tags:
- installs
- linux
- powershell
---
### Ubuntu
```shell
sudo apt update
sudo apt install -y wget apt-transport-https software-properties-common
wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
sudo dpkg -i packages-microsoft-prod.deb
sudo apt update
sudo apt install -y powershell
```

### Debian 11
```shell
sudo apt update && sudo apt install -y curl gnupg apt-transport-https
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-bullseye-prod bullseye main" > /etc/apt/sources.list.d/microsoft.list'
sudo apt update && sudo apt install -y powershell
```

# PowerCLI
```powershell
Install-Module VMware.PowerCLI
```

---
See also:
- [[Uninstall all VMware Powershell modules]]