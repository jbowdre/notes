---
tags:
  - git
---
Clone repo with submodules:
```shell
git clone --recurse-submodules git@github.com:jbowdre/runtimeterror.git
```

Pull submodules into local repo:
```shell
git submodule update --init --recursive
```

Update submodules:
```
git submodule update --remote --merge
```