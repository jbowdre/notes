---
tags:
  - windows
  - activedirectory
  - powershell
  - troubleshooting
---
```powershell
Test-ComputerSecureChannel
Reset-ComputerMachinePassword -Server $domain_controller -Credential $domain\$admin_user
```
