---
tags:
  - vmware
  - powercli
  - powershell
---
After years of development/experimentation, I wound up with a *ton* of outdated VMware Powershell modules installed, and wanted to remove them all in one go.

> The same basic approach would work for removing all modules which match a naming pattern, not just VMware ones.

```powershell
Function Uninstall-VMwareModules {
  $Modules = @()
  $Modules += (Get-Module -ListAvailable VMware.*).Name
  If (($Modules.Count - 1) -gt 0) {
    Write-Host ($Modules.Count - 1) "VMware modules found."
    $Modules | ForEach-Object -Parallel {
      Write-Host "Uninstalling $PSItem..."
      Uninstall-Module $PSItem -Force
    }
  } Else {
    Write-Host "No VMware modules found."
    Exit
  }
}
Uninstall-VMwareModules
Write-Host "Running again to remove any stragglers..."
Uninstall-VMwareModules
```

---
See also:
- [[powershell and powercli]]