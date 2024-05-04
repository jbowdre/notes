---
tags:
  - vmware
  - powercli
  - powershell
---

```powershell
$linuxVms = foreach( $datacenter in ( Get-Datacenter )) {
  Get-Datacenter $datacenter | Get-VM | Where { $_.ExtensionData.Config.GuestFullName -notmatch "win" -and $_.Name -notmatch "vcls" } | `
  Select @{ N="Datacenter";E={ $datacenter.Name }},
  Name,
  Notes,
  @{ N="Configured OS";E={ $_.ExtensionData.Config.GuestFullName }},  # OS based on the .vmx configuration
  @{ N="Running OS";E={ $_.Guest.OsFullName }}, # OS as reported by VMware Tools
  @{ N="Powered On";E={ $_.PowerState -eq "PoweredOn" }},
  @{ N="IP Address";E={ $_.ExtensionData.Guest.IpAddress }}
}
$linuxVms | Export-Csv -Path ./linuxVms.csv -NoTypeInformation -UseCulture
```
