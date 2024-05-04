---
tags:
  - powershell
  - activedirectory
  - windows
---
# Manage MS DNS records

### Create:
```powershell
Add-DnsServerResourceRecordA -ComputerName $dns_server -ZoneName $domain_name -CreatePtr -Name $record_name -IPv4Address $ip_address
```

### Delete:
```powershell
Remove-DnsServerResourceRecord -ComputerName $dns_server -ZoneName $domain_name -Name $record_name -RRType A -Force
```