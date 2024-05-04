---
tags:
  - vmware
  - powercli
---
### Create
```powershell
Get-VM $vm_name_filter | New-Snapshot -Name $snapshot_name -Description "Created $(Get-Date) for $reason" -Quiesce -RunAsync

```

### Delete
```powershell
Get-VM $vm_name_filter | Get-Snapshot -Name $snapshot_name | Remove-Snapshot -Confirm:$false -RunAsync
```
