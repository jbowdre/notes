---
tags:
  - linux
  - networking
  - packages
---
TCP/SYN port scan (default)
```shell
nmap $target -sS
```

TCP port scan without root
```shell
nmap $target -sT
```

Skip discovery ping
```shell
nmap $target -Pn
```

Ping scan only
```shell
nmap $target -sn
```

Report why port open/closed
```shell
nmap $target -reason
```

Enable OS detection
```shell
nmap $target -O
```

Enable OS detection, version detection, script scanning, traceroute
```shell
nmap $target -A
```

Attempt to determine version of service on a port
```shell
nmap $target -sV
```

Use tiny fragmented IP packets
```shell
nmap $target -f
```

Set custom MTU size
```shell
nmap $target -mtu [value]
```