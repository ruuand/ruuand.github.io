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

## Interforests Trusts
Par défaut une trust entre deux forêt n'ouvre aucun accès particulier. Cependant il faut tenir compte de certains éléments:
- La désactivation du SID Filtering ouvre la possibilité d'usurper des identités avec le SIDHistory
- Le groupe "Authenticated Users" est calculé de manière dynamique. Il va inclure les utilisateurs de toutes les forêts auxquelles on fait confiance.
- Donner des accès en administrateur sur un serveur (de la forêt A) à un utilisateur d'une autre forêt (forêt B) crée un risque pour les deux forêts
  - L'utilisateur de B pourra faire du mimikatz sur le serveur de A et récupérer des credentials
  - Un administrateur sur le serveur de A pourra récupérer les credentials de l'utilisateur de B

Références
----------
- [Articles de harmj0y](http://www.harmj0y.net/blog/tag/domain-trusts/)
