---
tags:
  - cloudflare
  - docker
  - containers
---
```yaml
# docker-compose.yml
services
  cloudflared: 
    image: cloudflare/cloudflared
    container_name: speedtest-cloudflared
    restart: unless-stopped
    command:
      - tunnel
      - --no-autoupdate
      - run
      - --token
      - ${CLOUDFLARED_TOKEN}
  speedtest:
    image: openspeedtest/latest
    container_name: speedtest
    restart: unless-stopped
    network_mode: service:cloudflared
```

---
See also:
- [[Tailscale serve in docker compose]]