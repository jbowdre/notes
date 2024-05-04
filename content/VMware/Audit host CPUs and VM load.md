---
tags:
  - vmware
  - powercli
---
```powershell
Get-VMhost | % {
  $vmHost = $_
  $socketCount = Get-View -ViewType HostSystem -Property Hardware.CpuInfo -Filter @{"Name"="$vmHost"} | Select @{n="NumCpuSockets";e={$_.Hardware.CpuInfo.NumCpuPackages}}
  New-Object -Type PSObject -Property @{
    HostName = $vmHost.Name
    SocketCount = $socketCount.NumCpuSockets
    VMCount = ($vmHost | Get-VM).count
    IsStandalone = $vmHost.IsStandalone
    Parent = $vmHost.Parent
  }
} | Select HostName, SocketCount, VMCount, IsStandalone, Parent | Sort HostName | Export-Csv -NoTypeInformation ./ESXi_Socket_Info.csv
```
