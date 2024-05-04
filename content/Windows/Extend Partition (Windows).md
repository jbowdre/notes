---
tags:
  - windows
  - powershell
  - disk
---
```powershell
$part = Get-Volume -DriveLetter C | Get-Partition
$part | Resize-Partition -Size ($part | Get-PartitionSupportedSize).sizeMax
```
---
See also:
- [[LVM crash course]]