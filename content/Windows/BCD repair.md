---
tags:
  - windows
  - troubleshooting
---
```shell
bootrec /FixMbr
bootrec /FixBoot
bootrec /ScanOs
bootrec /RebuildBcd
# If 0 installations found:
bcdedit /export c:\bcdbackup
attrib c:\boot\bcd - -r -s
ren c:\boot\bcd bcd.old
bootrec /RebuildBcd
```
