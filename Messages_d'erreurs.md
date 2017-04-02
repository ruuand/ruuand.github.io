---
title: Messages d'erreurs
permalink: /Messages_d'erreurs/
---

# Messages d'erreurs

Cette page regroupe des informations sur les messages d'erreurs qui peuvent être une source de données très utile en test d'intrusion.

PHP
---

Il est possible de provoquer des erreurs en passant un array et non un string dans les paramètres de la requête GET/POST:

``` text
REQUÊTE:
challenge01.root-me.org/web-serveur/ch31/?action=members&id[]=0

REPONSE:
Warning: file_exists() expects parameter 1 to be a valid path, string given in /challenge/web-serveur/ch15/ch15.php on line 32
```

[Catégorie:Méthodologies](/Catégorie:Méthodologies "wikilink")
