---
tags:
  - powercli
  - vmware
---

Enable:
```powershell
Get-VMHostService -VMHost $host | ? {$_.Key -eq "TSM-SSH"} | Start-VMHostService
```

Disable:
```powershell
Get-VMHostService -VMHost $host | ? {$_.Key -eq "TSM-SSH"} | Stop-VMHostService
```