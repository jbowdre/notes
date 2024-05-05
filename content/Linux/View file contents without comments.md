---
tags:
  - linux
  - shell
---
Strips out lines which start with `#`:
```shell
egrep -v "^\s*(#|$)" $filename 
```

More convenience:
```shell
alias ccat='egrep -v "^\s*(#|$)"'
```
