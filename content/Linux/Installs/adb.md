---
tags:
- installs
- android
- linux
---

```shell
wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip
cd platform-tools
sudo install adb /usr/local/bin/
sudo install fastboot /usr/local/bin/
cd && rm -rf platform-tools*
```
