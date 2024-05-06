---
tags:
  - vmware
---
To add vSAN witness traffic to a vmkernel interface of a host; useful in 2-node configs where the witness traffic should traverse the management interface:

```shell
esxcli vsan network ip add -i vmk0 -T=witness
```