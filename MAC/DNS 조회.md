---
tags:
  - DNS
  - MAC
date: 2026-01-07
---


## CLI

```bash

$ dig {domain} NS 
$ dig {domain} +short NS

$ nslookup -type=NS {domain}

$ host -t NS {domain}


$ whois example.com | grep "Name Server"

```

