---
title: SNMP
permalink: /SNMP/
---

Outils
------

Différents outils sont disponibles en lien avec le protocole SNMP.

### nmap

Un scan **nmap** permet d'identifier la présence d'un service SNMP

``` bash
nmap -sU --open -p 161 192.168.31.201
```

### onesixtyone

L'outil **onesixtyone** permet de tester les communities sur une plage d'IPs. Les fichiers community.txt et ips.txt contiennent les éléments à tester:

``` bash
onesixtyone -c community.txt -i ips.txt
```

### snmpwalk

L'outil **snmpwalk** permet de récupérer des informations à partir de snmp:

``` bash
snmpwalk -c public -v1 192.168.31.222
```

### snmp-check

``` bash
snmp-check 192.168.101.196 -c public
```

[Category:Protocoles](/Category:Protocoles "wikilink")