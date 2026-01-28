# SAN Certificate CSR + Key Creation (OpenSSL)

This runbook generates a **new private key** and a **CSR with SAN entries** for SSL/TLS certificate issuance.

---

## 1) Prerequisites
- OpenSSL installed (Mac/Linux usually comes default)
- A SAN config file (`.conf`) ready

## Check OpenSSL:
openssl version

## Generate Private Key + CSR (SAN Enabled)
openssl req -new -newkey rsa:2048 -nodes \
  -keyout example_com_2026.key \
  -out example_com_2026.csr \
  -config example_2026.conf

## Verify CSR Subject (CN)
  openssl req -in example_com_2026.csr -noout -subject
  
## Verify CSR contains SAN
  openssl req -in example_com_2026.csr -noout -text | grep -A2 "Subject Alternative Name"




