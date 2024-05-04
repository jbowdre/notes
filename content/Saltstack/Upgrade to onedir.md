---
tags:
  - salt
---
## Ubuntu

Import new key:
```shell
sudo curl -fsSL -o /usr/share/keyrings/salt-archive-keyring-2023.gpg https://repo.saltproject.io/salt/py3/ubuntu/20.04/amd64/SALT-PROJECT-GPG-PUBKEY-2023.gpg
```

Update `/etc/apt/sources.list.d/salt.list`
```shell
deb [signed-by=/usr/share/keyrings/salt-archive-keyring-2023.gpg] https://repo.saltproject.io/salt/py3/ubuntu/20.04/amd64/latest focal main
```

Update:
```shell
sudo apt-get update && sudo apt-get upgrade salt-minion -y
```

## Re-bootstrap existing minion
```shell
sudo salt 'minion' cmd.shell 'curl -L https://bootstrap.saltproject.io | sh -s -- onedir'
```