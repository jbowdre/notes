---
tags:
  - linux
  - shell
---
That is, the interface which is attached to the default route

```shell
ip addr show $(ip route | grep default | awk '{print $5}') | grep 'inet ' | awk '{print $2}' | cut -d/ -f1
```

