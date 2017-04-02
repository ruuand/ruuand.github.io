---
title: SNMP
permalink: /SNMP/
---

# Simple Network Management Protocol

## Outils

Différents outils sont disponibles en lien avec le protocole SNMP.

### nmap

Un scan **nmap** permet d'identifier la présence d'un service SNMP

``` bash
[~] nmap -sU --open -p 161 192.168.31.201
```

Il est également possible d'utiliser des scripts nmap pour brute forcer les community strings.

### onesixtyone

L'outil **onesixtyone** permet de tester les communities sur une plage d'IPs. Les fichiers community.txt et ips.txt contiennent les éléments à tester:

``` bash
[~] onesixtyone -c community.txt -i ips.txt
```

## Post Exploitation
Dans le cas d'une communauté "READ" on peut récupérer des information sur la configuration.

``` bash
[~] snmpwalk -c public -v1 192.168.31.222
[~] snmp-check 192.168.101.196 -c public # Résultat plus "user friendly"
```

Dans le cas d'une communauté "READ/WRITE" on peut effectuer des modifications.

``` bash
[~] snmpset -v 2c -c demopublic test.net-snmp.org ucdDemoPublicString.0 s "hello world"
enterprises.ucdavis.ucdDemoMIB.ucdDemoMIBObjects.ucdDemoPublic.ucdDemoPublicString.0 = "hello world"
```

Des modules metasploit existent également pour lister les informations et modifier les
paramètres.
