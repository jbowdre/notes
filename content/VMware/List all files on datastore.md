---
tags:
  - vmware
  - powercli
---
```powershell
$ds = Get-Datastore -Name $datastore_name
New-PSDrive -Location $ds -Name DS -PSProvider VimDatastore -Root '\'
$report = Get-ChildItem Path DS:\ -Recurse | Select Name, Length, FolderPath
$report | Export-Csv -NoTypeInformation -Path ./report.csv
Remove-PSDrive -Name DS -Confirm:$false
```
