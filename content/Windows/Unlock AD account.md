---
tags:
  - activedirectory
  - windows
  - powershell
---
```powershell
Get-AdUser -Identity $username -Properties LockedOut | Select-Object Name, LockedOut
Unlock-AdAccount -Identity $username
```

  