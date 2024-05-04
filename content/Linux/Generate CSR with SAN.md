---
tags:
  - linux
  - certificates
  - ssl
---
1. Generate server private key
```shell
openssl genrsa -out harbor.lab.bowdre.net.key 4096
```
2. Generate configuration file `csr.conf`
```
[ req ]
default_bits = 4096
distinguished_name = req_distinguished_name
req_extensions = v3_req
prompt = no

[ req_distinguished_name ]
C = US
ST = Alabama
L = Huntsville
O = runtimeterror.dev
OU = notes
CN = $(hostname)

[ v3_req ]
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
extendedKeyUsage = serverAuth
subjectAltName = @alt_names

[ alt_names ]
DNS.1 = $(hostname)
DNS.2 = $(hostname -s)
DNS.3 = $(hostname -i)
```
3. Generate CSR
```shell
openssl req -new -out harbor.lab.bowdre.net.csr -key harbor.lab.bowdre.net.key -config csr.conf
```

---
See also:
- [[OpenSSL Cheatsheet]]