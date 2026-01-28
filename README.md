# SAN Certificate CSR + Key Creation (OpenSSL)

This runbook generates a **new private key** and a **CSR with SAN entries** for SSL/TLS certificate issuance.

OpenSSL CSR + SAN config templates used for certificate renewals.

## Contents
- CSR generation examples
- SAN config templates
- Validation commands

## Security
Never commit private keys (*.key), PFX (*.pfx/*.p12), or cert bundles containing private material.

---

## 1) Prerequisites
- OpenSSL installed (Mac/Linux usually comes default)
- A SAN config file (`.conf`) ready

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




