# SAN Certificate CSR + Key Creation (OpenSSL)

This runbook generates a **new private key** and a **CSR with SAN entries** for SSL/TLS certificate issuance.

OpenSSL CSR + SAN config templates used for certificate renewals.
---

## Contents
- CSR generation examples
- SAN config templates
- Validation commands
---

## Security
Never commit private keys (*.key), PFX (*.pfx/*.p12), or cert bundles containing private material.

---

## Prerequisites
- OpenSSL installed (Mac/Linux usually comes default)
- A SAN config file (`.conf`) ready
  
---

## Check OpenSSL:
```bash
openssl version
```

## Generate Private Key + CSR (SAN Enabled)
```bash
openssl req -new -newkey rsa:2048 -nodes \
  -keyout server.key \
  -out server.csr \
  -config example.conf
```

## Verify CSR Subject (CN)
```bash
  openssl req -in server.csr -noout -subject
```
  
## Verify CSR contains SAN
```bash
  openssl req -in server.csr -noout -text | grep -A2 "Subject Alternative Name"
```

## Convert Cert and Key Files into PFX
```bash
  openssl pkcs12 -export \
  -out certificate.pfx \
  -inkey private.key \
  -in certificate.crt \
  -certfile ca-bundle.crt
```

## Extract Cert from PFX
```
openssl pkcs12 -in yourfile.pfx -clcerts -nokeys -out certificate.crt
```

## Extract Key from PFX
```
openssl pkcs12 -in yourfile.pfx -nocerts -nodes -out private.key
```

