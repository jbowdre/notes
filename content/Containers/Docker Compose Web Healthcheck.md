---
tags:
  - docker
  - containers
---
Basic healthcheck for a basic web service.

### curl:

```yaml
services:
  cyberchef:
    container_name: cyberchef
    image: mpepping/cyberchef:latest
    restart: unless-stopped
    network_mode: service:tailscale
    healthcheck:
      test: curl --fail http://localhost:8000 || exit 1
      interval: 60s
      retries: 5
      start_period: 20s
      timeout: 10s
```

### wget:

```yaml
services:
  cyberchef:
    container_name: cyberchef
    image: mpepping/cyberchef:latest
    restart: unless-stopped
    network_mode: service:tailscale
    healthcheck:
      test: wget --no-verbose --tries=1 --spider http://localhost:8080 || exit 1
      interval: 60s
      retries: 5
      start_period: 20s
      timeout: 10s
```