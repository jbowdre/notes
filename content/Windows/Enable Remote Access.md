---
tags:
  - windows
  - powershell
---
### RDP, WMI, File/Printer sharing firewall rules
```powershell
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
Enable-NetFirewallRule -DisplayGroup "Windows Management Instrumentation (WMI)"
Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"
```

### PowerShell remoting
```powershell
Enable-PsRemoting
```

### Enable Remote Desktop
```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```
