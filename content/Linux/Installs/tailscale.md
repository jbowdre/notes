---
tags:
- installs
- linux
- tailscale
---
```shell
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up --accept-routes --ssh --advertise-tags="tag:client"
```

### Manual install
Check https://pkgs.tailscale.com/stable/#static for the latest version
```shell
wget https://pkgs.tailscale.com/stable/tailscale_VERSION_ARCH.tgz
tar xvf tailscale_VERSION_ARCH.tgz
sudo install -m 755 tailscale_VERSION_ARCH/tailscale /usr/bin/
sudo install -m 755 tailscale_VERSION_ARCH/tailscaled /usr/sbin/
sudo install -m 644 tailscale_VERSION_ARCH/systemd/tailscaled_defaults /etc/defaults/tailscaled
sudo install -m 644 tailscale_VERSION_ARCH/systemd/tailscaled.service /usr/lib/systemd/system/
sudo systemctl enable tailscaled
sudo systemctl start tailscaled
```