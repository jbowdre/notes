---
tags:
  - docker
  - containers
---
[Watchtower](https://containrrr.dev/watchtower) is useful for automatically updating (and restarting) Docker containers.

Example:
```shell
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower
```

Tell it to only manage certain containers:
```shell
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower \
  nginx redis
```

Compose:
```yaml
services:
  watchtower:
    container_name: watchtower
    image: containrrr/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
