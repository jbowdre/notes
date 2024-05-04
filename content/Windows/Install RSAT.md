---
tags:
  - windows
  - powershell
  - installs
---
List available tools:
```powershell
Get-WindowsCapability -Name RSAT* -Online | Select-Object -Property Name, State
```

Install an individual tool:
```powershell
Add-WindowsCapability -Name Rsat.FileServices.Tools~~~~0.0.1.0
```

Or install all of them:
```powershell
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```