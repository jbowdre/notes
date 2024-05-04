---
tags:
  - installs
  - linux
  - golang
---
Download from https://go.dev/dl/:
```shell
wget https://go.dev/dl/go${VERSION}.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go${VERSION}$.linux-amd64.tar.gz
mkdir ~/go
export GOPATH=$HOME/go
export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
```
