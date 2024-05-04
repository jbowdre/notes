---
tags:
  - containers
  - kubernetes
---
### View
For encoded `values.yaml` key
```shell
kubectl -n $namespace get secret $secret -o yaml | awk '/values.yaml/ {print $2}' | base64 --decode > secret.yaml
```

### Modify
Make changes to `secret.yaml`, then
```shell
kubectl -n $namespace patch secret $secret -p '{"data": {"values.yaml": "'''$(base64 -w 0 secret.yaml)'''"}}'
```

>[!INFO] Avoid newlines
>The `-w 0`/`--wrap=0` argument tells `base64` to *not* wrap the encoded lines after a certain number of characters. If you leave this off, the string gets a newline inserted every 76 characters and `kubectl` will puke when trying to parse it.
