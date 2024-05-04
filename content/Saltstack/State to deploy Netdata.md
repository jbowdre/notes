---
tags:
  - "#salt"
  - "#tailscale"
---
Deploys [netdata](https://github.com/netdata/netdata) and publishes it with [Tailscale Serve](https://tailscale.com/kb/1242/tailscale-serve)

```yaml
# -*- coding: utf-8 -*-
# vim: ft=sls
# Hasty Salt config to install Netdata and make it available within a tailnet
# at https://[hostname].[tailnet-name].ts.net:8443/netdata

curl:
  pkg.installed

tailscale:
  pkg.installed:
    - version: latest

netdata-kickstart:
  cmd.run:
    - name: curl -Ss https://get.netdata.cloud/kickstart.sh | sh -s -- --dont-wait
    - require:
      - pkg: curl
    # don't run this block if netdata is already running
    - unless: pgrep netdata

tailscale-serve:
  cmd.run:
    - name: tailscale serve --bg --https 8443 --set-path /netdata 19999
    - require:
      - pkg: tailscale
      - cmd: netdata-kickstart
    # don't run this if netdata is already tailscale-served
    - unless: tailscale serve status | grep -q '/netdata proxy http://127.0.0.1:19999'

```
