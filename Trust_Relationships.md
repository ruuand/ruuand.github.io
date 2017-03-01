---
title: Trust Relationships
permalink: /Trust_Relationships/
---

# Trust Relationships

Les relations d'approbation permettent à plusieurs domaines de communiquer entre eux.

Elevation de priviléges
-----------------------
Plusieurs outils permettent de profiter des relations d'approbations pour élever ses priviléges, notamment en partant d'un domaine enfant vers un domaine parent. Ceci exploite notamment les "SIDHistory". Plusieurs outils permettent d'exploiter ce problème:
- raiseChild.py de la suite Impacket

Il est possible d'utiliser le mécanisme de "SID Filtering" pour limiter ce type d'attaque. Cependant, l'utilisation de ce mécanisme ne doit pas se faire au sein d'une même forêt, ce qui peut causer des problèmes de réplication (voir http://windowsitpro.com/windows-server/exploiting-sidhistory-ad-attribute). En gros, il vaut mieux mettre le domaine dans une forêt séparée si on ne lui fait pas confiance.

Références
----------
- [Articles de harmj0y](http://www.harmj0y.net/blog/tag/domain-trusts/)
