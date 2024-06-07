---
tags:
  - linux
  - ssl
  - troubleshooting
---
When attempting to curl *anything* returns something like
```
curl: (35) error:0A000152:SSL routines::unsafe legacy renegotiation disabled
```

Edit `/usr/lib/ssl/openssl.cnf`:
```
[openssl_init]
# comment out:
# providers = provider_sect

# insert:
ssl_conf = ssl_sect

[ssl_sect]
system_default - system_default_sect

[system_default_sect]
Options = UnsafeLegacyRenegotiation

[provider_sect]
default = default_sect
```
