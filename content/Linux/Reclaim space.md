---
tags:
  - linux
  - shell
  - disk
---
### Find largest files
```shell
du -a /path/ | sort -n -r | head -n 20
```

### Delete logs older than 30 days
```shell
find /path/ -type f -name "*log*" -mtime +30 -ls
find /path/ -type f -name "*log*" -mtime +30 -exec rm {} \;
```