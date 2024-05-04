---
tags:
  - salt
  - linux
---
Refresh `gitfs` file server
```shell 
salt-run fileserver.update
```

Display content of  `salt://` filesystem
```shell
salt-run fileserver.file_list
```

Show minion highstate
```shell
salt '*' state.show_top
```

Apply minion highstate
```shell
salt '*' state.highstate
```

List available modules
```shell
salt '*' sys.list_modules
```

List available functions for a given module
```shell
salt '*' sys.list_functions <module_name>
```

Inline documentation
```shell
salt '*' sys.doc <module_name>
salt '*' sys.doc <module_name>.<function_name>
```

Encrypt data to store in pillar:
```shell
sudo apt install -y rng-tools
sudo mkdir /etc/salt/gpgkeys
sudo chmod 700 /etc/salt/gpgkeys
sudo gpg --gen-key  --homedir /etc/salt/gpgkeys --passphrase '' --pinentry-mode loopback
sudo gpg  --homedir /etc/salt/gpgkeys/ --armor  --export saltmaster > ~/exported_pubkey.gpg
gpg --import exported_pubkey.gpg
echo -n "jbpass" | gpg  --armor --trust-model always --encrypt -r saltmaster
```

