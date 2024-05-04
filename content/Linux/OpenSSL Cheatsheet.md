---
tags:
  - linux
  - certificates
  - ssl
---
# OpenSSL Cheatsheet
### Formats
Base64 == PEM
Binary == DER

### Export .p7b chain into .cer bundle
p7b has all the certs collapsed into a single one; this will break them back out into individual certs again
```shell
openssl pkcs7 -inform DER -outform PEM -in chain.p7b -print_certs > cert_bundle.crt
```

### Retrieve cert from web server
```shell
openssl s_client -showcerts $serverFqdn:443 </dev/null 2>/dev/null | openssl x509 -outform PEM > certificate.crt
```

### View certificate information
```shell
openssl x509 -in certificate.crt -text -noout
```

### Generate standard CSR
```shell
openssl req -new \
-newkey rsa:4096 -nodes -keyout hostname.key \
-out hostname.csr \
-subj "/C=US/ST=Alabama/L=Huntsville/O=example.com/OU=LAB/CN=hostname.example.com"
```
For CSR w/ SAN:
[[Generate CSR with SAN]]

### Review CSR
```shell
openssl req -text -noout -verify -in csr.csr
```

---
See also:
- [[Generate CSR with SAN]]
