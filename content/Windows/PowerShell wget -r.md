---
tags:
  - windows
  - powershell
---
To download all the files in a web file server directory (with directory browsing enabled, of course)

```powershell
$outputdir = 'C:\Scripts\Download\'
$url = 'https://example.com/stuff/files/'

# enable TLS 1.2 and TLS 1.1 protocols
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12, [Net.SecurityProtocolType]::Tls11

$WebResponse = Invoke-WebRequest -Uri $url
# get the list of links, skip the first one ("[To Parent Directory]") and download the files
$WebResponse.Links | Select-Object -ExpandProperty href -Skip 1 | ForEach-Object {
    $fileName = $_.ToString().Split('/')[-1]                        # 'filename.ext'
    $filePath = Join-Path -Path $outputdir -ChildPath $fileName     # 'C:\Scripts\Download\filename.ext'
    $baseUrl = $url.split('/')                                      # ['https', '', 'example.com', 'stuff', 'files']
    $baseUrl = $baseUrl[0,2] -join '//'                             # 'https://example.com'
    $fileUrl  = '{0}{1}' -f $baseUrl.TrimEnd('/'), $_               # 'https://example.com/stuff/files/filename.ext'
    Invoke-WebRequest -Uri $fileUrl -OutFile $filePath
}
```