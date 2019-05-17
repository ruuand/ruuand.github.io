---
title: BloodHound
permalink: /BloodHound/
---

# BloodHound

## Utilisation

Tout passe par l'ingestor Sharphound.exe.

## Cypher queries

Quelques requêtes Cypher qui peuvent être utiles (inspiré de https://gist.github.com/jeffmcjunkin/7b4a67bb7dd0cfbfbd83768f3aa6eb12):

``` 
# Liste de tous les utilisateurs avec des droits d'admins locaux (direct ou via un groupe)
MATCH p=(u:User)-[r:AdminTo|MemberOf*1..]->(c:Computer) RETURN p

# Juste les groupes
MATCH p=(g:Group)-[r:AdminTo|MemberOf*1..]->(c:Computer) RETURN p

# Admin direct (sans groupe)
MATCH p=(u:User)-[r:AdminTo]->(c:Computer) RETURN p
```

## Hardening

Il est possible d'empêcher l'énumération des sessions locales avec l'outil [NetCease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)

## Ressources

-   [Projet Github](https://github.com/adaptivethreat/BloodHound)
-   [BloodHound - Custom Queries](http://www.securityripcord.com/blog/2016/09/28/bloodhound-custom-queries/)
-   [Extending BloodHound: Track and Visualize Your Compromise](http://porterhau5.com/blog/extending-bloodhound-track-and-visualize-your-compromise/)
-   [The ACL Attack Path Update](https://wald0.com/?p=112)
