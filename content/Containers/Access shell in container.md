---
tags:
  - kubernetes
  - docker
  - containers
---
### Kubernetes
```shell
kubectl -n $namespace exec -it $pod -- /bin/bash
```

> [!Note] Double-dash
> The double dash (`--`) separates the args passed to the command from the kubectl args

### Docker
```shell
docker exec -it $container /bin/bash
```
