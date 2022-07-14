---
layout: post
title:  "Create a CA and sign a CSR"
date:   2022-07-13 03:25:00 -0600
author: Leo
categories: certificates
---

Every now and then I have to create a CA to sign a CSR that I need to test with and end up googling the steps several times over. To save future me some time, I'll just write down the commands here.

This assumes I already have a CSR. Maybe I'll add a section on how to make a CSR later.

## Making a CA
1. Make the key for the Certificate Authority
```bash
openssl genrsa -out MyRootCA.key 2048
```
2. Create certificate using the new key we just made
```bash
openssl req -x509 -new -nodes -key MyRootCA.key -sha256 -days 1024 -out MyRootCA.pem
```
3. Sign CSR with the new Certificate Authority
```bash
openssl x509 -req -in MyClient1.csr -CA MyRootCA.pem -CAkey MyRootCA.key -CAcreateserial -out MyClient1.pem -days 1024 -sha256
```
4. Done!