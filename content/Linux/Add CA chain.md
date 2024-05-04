---
tags:
  - linux
  - certificates
  - ssl
---
1. Download certificate in PEM (b64) format
2. Copy certificate to `/usr/local/share/ca-certificates/$CERT_NAME.crt`.
3. `sudo update-ca-certificates`.
4. Look through `/etc/ssl/certs/ca-certificates/` to confirm it was added.
