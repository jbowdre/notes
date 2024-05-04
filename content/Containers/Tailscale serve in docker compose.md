---
tags:
  - tailscale
  - docker
  - containers
---
Define serve config:
```json
// serve-config.json
{
  "TCP": {
    "443": {
      "HTTPS": true
    }
  },
  "Web": {
    "hostname.tailnet-name.ts.net:443": {
      "Handlers": {
        "/": {
          "Proxy": "http://127.0.0.1:8000"
        }
      }
    }
  }//, uncomment to enable funnel
  // "AllowFunnel": {
  //   "hostname.tailnet-name.ts.net:443": true
  // }
}
```

Create deployment:
```yaml
services:
  tailscale:
    image: tailscale/tailscale:latest 
    container_name: cyberchef-tailscale
    restart: unless-stopped
    environment:
      TS_AUTHKEY: ${TS_AUTHKEY:?err}
      TS_HOSTNAME: ${TS_HOSTNAME:-ts-docker}
      TS_EXTRA_ARGS: ${TS_EXTRA_ARGS:-}
      TS_STATE_DIR: /var/lib/tailscale/
      TS_SERVE_CONFIG: /config/serve-config.json 
    volumes:
      - ./ts_data:/var/lib/tailscale/
      - ./serve-config.json:/config/serve-config.json 

  cyberchef:
    container_name: cyberchef
    image: mpepping/cyberchef:latest
    restart: unless-stopped
    network_mode: service:tailscale
```


