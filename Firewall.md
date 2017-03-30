---
title: Firewall
permalink: /Firewall/
---

# Firewall
Après avoir compromis un serveur on peut se retrouver bloqué pour l'établissement d'un shell.
Généralement on ne pourra pas faire de bind shell, et parfois pas de reverse shell non plus.
Les ports qui seront souvent ouverts:
- 80, 443 (HTTP / HTTPS)
- 53 (DNS)

Il est possible d'utiliser le payload meterpreter/reverse_all_ports pour tester
un plus grand nombre de ports si on ne sait pas lesquels passent. Il faut alors
mettre une régle iptable (ou autre) pour rediriger le trafic.

``` bash
iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 4444:9000 -j DNAT --to-destination
192.168.1.101:443 # Tiré de pentestercademy
```
