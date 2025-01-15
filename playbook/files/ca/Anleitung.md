## SSL-Zertifikate generieren
Sollte normalerweise über die Ansible-Rolle gemacht werden, im Notfall per Hand

1. Die beiden Dateien in playbooks/ca entschlüsseln und ablegen
2. CSR generieren: ```openssl req -nodes -new -newkey rsa:4096 -keyout server-key.pem -out csr.csr -config req_csr.conf```
3. CSR mit der CA signieren ```openssl x509 -req -days 365 -set_serial 01 -in csr.csr -out server-cert.pem -CA ca.crt -CAkey ca.key -copy_extensions copyall```
