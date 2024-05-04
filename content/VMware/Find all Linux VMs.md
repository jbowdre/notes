---
tags:
  - vmware
  - powercli
---
```powershell
$linuxVMs = foreach($datacenter in (Get-Datacenter)) {
  Get-Datacenter $datacenter | Get-VM | Where {$_.ExtensionData.Config.GuestFullNAme -NotMatch "win" -And $_.Name -NotMatch "vcls"} | `
  Select @{N="Datacenter";E={$datacenter.Name}},
  Name,
  Notes,
  @{N="Configured OS";E={$_.ExtensionData.Config.GuestFullName}},
  @{N="Running OS";E={$_.Guest.OsFullName}},
  @{N="Powered On";E={$_.PowerState -eq "PoweredOn"}},
  @{N="IP Address";E={$_.ExtensionData.Guest.IpAddress}}
}
$linuxVMs | Export-CSV -NoTypeInformation -Path ./linuxvms.csv
```