---
title: nmap
permalink: /nmap/
---

#nmap
Nmap est un des outils les plus utiles dans la phase de reconnaissance.

Quelques commandes utiles:
``` bash
nmap -sS -sV -sC 192.168.1.0/24 -oA nmap_output
```

Options utiles
- -F: scan "light"
- -sV: lance des scripts permettant de récupérer des informations de version
- -sC: lance les scripts "default"
- -O: OS detection
- -A: lance détection de version, d'OS, traceroute et "script scanning"


