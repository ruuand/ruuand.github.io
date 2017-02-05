---
title: LLMNR
permalink: /LLMNR/
---

LLMNR et Netbios sont des protocoles de résolution de noms dans des environnements Windows.

Fonctionnement
--------------

Lors d'une résolution de nom, la machine d'un utilisateur contacte le serveur DNS. Si celui-ci ne renvoie pas de réponse, alors la machine envoie une requête LLMNR en multicast ou NetBIOS en broadcast.

Responder
---------

L'attaque "traditionnelle" consiste à répondre à toutes les résolutions de noms LLMNR/NetBIOS sur le réseau local. Ceci permet de forcer la machine d'un utilisateur à effectuer une connection sur notre machine. Il est alors possible de récupérer des credentials (ex: authentification HTTP, NetNTLMv2, etc.).

L'outil Responder permet de faire ce type d'attaque:

-   Répondre aux requêtes LLMNR/NetBIOS
-   Mettre en place des serveurs HTTP, SMB, etc. pour proposer une authentification

Il est également possible de lancer Responder via un outil en USB (l'authentification sera alors toujours demandée). La [LANTurtle](/LANTurtle "wikilink") permet de faire cela.

On peut ensuite casser les hashs NetNTLMv2 obtenus avec [hashcat](/hashcat "wikilink").

### Défenses

Il est possible de désactiver LLMNR et NetBIOS pour empêcher ce type d'attaque. Ces protocoles ne sont à priori pas nécessaire pour un fonctionnement normal dans un environnement Active Directory.

[Category:Outils](/Category:Outils "wikilink")[Category:Protocoles](/Category:Protocoles "wikilink")