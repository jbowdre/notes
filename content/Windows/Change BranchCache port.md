---
tags:
  - "#windows"
---
When enabled, [BranchCache](https://learn.microsoft.com/en-us/windows-server/networking/branchcache/branchcache) defaults to listening on port `80` which may interfere with other web services. Here's how to shift it to a different port (`8081` in this case)

```shell
# confirm that a system process is listening on 80
netstat -ano | findstr /c:":80 "
TCP   0.0.0.0:80    0.0.0.0:0    LISTENING    4

# change service mode so we can modify it
netsh br set service mode=local

# change the port
reg add "HKLM\Software\Microsoft\Windows NT\CurrentVersion\PeerDist\DownloadManager\Peers\Connection" /v ListenPort /t REG_DWORD 8081 /f

# reset service mode
netsh br set service mode=distributed

# bounce the service
netsh stop peerdistsvc
netsh start peerdistsvc

# confirm that it's not on 80 anymore
netstat -ano | findstr /c:":80 "
```
