---
tags:
  - salt
---
Useful for remotely restarting a salt minion, uses `test.succeed_with_changes` to return a successful run even as the minion disconnects (and hopefully reconnects)

```yaml
# -*- coding: utf-8 -*-
# vim: ft=sls
# bounce the targeted salt-minion
---
test:
  test.succeed_with_changes

salt-minion:
  cmd.run:
    - name: 'sleep 10; salt-call service.restart salt-minion'
    - bg: True
    - reload_modules: True
    - onchanges:
      - test: test
```