---
title: Trust Relationships
permalink: /Trust_Relationships/
---

# Trust Relationships

Les relations d'approbation permettent à plusieurs domaines de communiquer entre eux.

## Elevation de priviléges
Plusieurs outils permettent de profiter des relations d'approbations pour élever ses priviléges, notamment en partant d'un domaine enfant vers un domaine parent. Ceci exploite notamment les "SIDHistory". L'outil **raiseChild.py** présent dans impacket fait cela:
```
raiseChild.py jenova.shinra-inc.local/Administrator -target-exec 192.168.56.101 # Passe du sous-domaine jenova.shinra-inc.local au domaine shinra-inc.local et lance un psexec sur le serveur 192.168.56.101
```

Il est également possible de s'en sortir avec mimikatz en générant un golden ticket qui inclut les SID History du groupe Enterprise Admin du domaine parent. C'est en revanche un peu plus laborieux.

## SID Filtering
Il est possible d'utiliser le mécanisme de "SID Filtering" pour limiter ce type d'attaque. Cependant, l'utilisation de ce mécanisme ne doit pas se faire au sein d'une même forêt, ce qui peut causer des problèmes de réplication (voir http://windowsitpro.com/windows-server/exploiting-sidhistory-ad-attribute). En gros, il vaut mieux mettre le domaine dans une forêt séparée si on ne lui fait pas confiance.

Références
----------
- [Articles de harmj0y](http://www.harmj0y.net/blog/tag/domain-trusts/)
