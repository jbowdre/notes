---
tags:
- containers
- docker
---
If you've got a container managed by Docker Compose which you'd like to restart on a regular (say, daily) basis:

```yaml
services:
  unreliable_app:
    container_name: unreliable_app
    image: nginx:alpine
    ports: ["80:80"]
    restart: unless-stopped

  restarter:
    image: docker:cli
    volumes: ["/var/run/docker.sock:/var/run/docker.sock"]
    command: ["/bin/sh", "-c", "while true; do sleep 86400; docker restart unreliable_app; done"]
    restart: unless-stopped
```
