---
tags:
  - "#linux"
  - packages
  - ubuntu
  - debian
---
Finding a package (online):
```shell
apt-cache search $search_string
```

Finding an installed package:
```shell
apt list --installed | grep $search_string
```

Finding what package a file came from:
```shell
dpkg -S /path/to/file
```

Finding what files a package provides:
```shell
dpkg -L $package_name
```