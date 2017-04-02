---
title: DHCP
permalink: /DHCP/
---

# DHCP

Attribution statique
--------------------
Pour attributer de manière statique une adresse IP
```text
  ifconfig eth0 192.168.1.22 up
  route add default gw 192.168.1.1 eth0
```
