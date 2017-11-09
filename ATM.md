---
title: ATM
permalink: /ATM/
---

# ATM

## Généralités

2 types d'applications dans un ATM (soit des softs fermés qui sont utilisables juste avec des ATMS spécifiques, soit des softs plus ouverts compatibles avec différentes machines.)

Windows Applications -> XFS APIS qui repose sur XFS SPIs (interaction avec les périphériques externes) -> Service Providers. (Voir le standard [CEN/XFS](https://en.wikipedia.org/wiki/CEN/XFS))

## Attaques

Plusieurs types d'attaques:

- Attaques physiques (skimming, trapping, etc.)
- Attaques logiques (se connecter sur l'ATM en accédant à de l'USB, Ethernet, etc. via l'ouverture de l'ATM).

Nombreux malwares ciblant des ATM (Ploutus, Padpin, Macau, Tyupkin, GreenDispenser, Rupper, Sucessfull, Alice):

- Vérifie la présence de MSXFS.dll (présent sur de nombreux ATM) (Voir https://github.com/vallejocc/PoC-Fake-Msxfs qui propose une fausse .dll pour intéragir avec les malwares bancaires).
- Fait un appel à l'API XFS Manager.
- Envoie des instructions aux périphériques via WFSexecute

Méthodologie de pentest en réutilisant des malwares connus:
- Avoir un malware connu
- Injecter le malware via un Live USB ou Live CD. Souvent le password du BIOS (s'il y en a un est celui par défaut.
- Les machines sont assez bavardes sur le réseau (Responder, arpspoof).
- Les machines sont une forme de kiosque. Il est possible de récupérer un invite de commande ou navigateur pour dl un malware / tools.
- Désactiver les protections :)
- Lancer le malware en mode debug afin de voir ce qu'il fait step by step.

Approche différentes:
- Coder un Soft à injecter dans des ATM. (Voir RootedCon)
- [Hack your ATM with friend's Raspberry.py](https://www.youtube.com/watch?v=q5tQWe6YsLM)
