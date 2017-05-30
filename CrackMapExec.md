---
title: CrackMapExec
permalink: /CrackMapExec/
---

# CrackMapExec

[CrackMapExec](/CrackMapExec "wikilink") est un outil d'exploitation en python (https://github.com/byt3bl33d3r/CrackMapExec).

Fonctionnalités
---------------

Plusieurs fonctionnalités:

-   Obtenir des informations sur des partages réseaux (--shares)
-   Executer des commandes basiques sur des serveurs (-x ipconfig)
-   Faire du mass mimikatz (-M mimikatz)
-   Faire du mass meterpreter en combinaison avec Empire ou metasploit (-M met_inject)
-   Bypass d'Applocker
-   Dumper les hashs locaux (--sam)
-   Stocker les informations dans une base de données (cmedb)

### Partages réseaux

Les fonctionnalités suivantes sont utiles pour rechercher des informations sur des partages réseaux:

``` bash
cme 192.168.10.0/24 -u user -p password --shares # Lister les shares et leur permission
cme 192.168.10.34 -u user -p password --spider --share ShareName --pattern pass # Chercher des fichier sensibles (recherche sur le nom)
cme 192.168.10.34 -u user -p password --spider --share ShareName --pattern pass --content # Chercher des fichier sensibles (recherche dans le contenu)
```

### Base de données

Une base de données stocke les informations obtenues.

Références
----------

-   [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec)
-   [Getting the goods with CrackMapExec part 1](https://byt3bl33d3r.github.io/getting-the-goods-with-crackmapexec-part-1.html)
-   [Getting the goods with CrackMapExec: Part 2](https://byt3bl33d3r.github.io/getting-the-goods-with-crackmapexec-part-2.html)
