---
title: ZIP
permalink: /ZIP/
---

# ZIP

Il est possible d'exploiter des vulnérabilités sur certains formulaires d'upload en uploadant des fichiers .zip si ceux-ci sont mal traités lors de la décompression.

## Exploitation
### Liens symboliques

On peut créer un lien symbolique vers un fichier auquel on a pas accès:

``` 
# Pour lire le contenu de index.php
ln -s ../index.php ./link.txt
zip --symlinks -r boom.zip ./link.txt
```

### Bombe ZIP

On peut faire un déni de service. Voir [Zip bomb](https://github.com/AbhiAgarwal/notes/wiki/Zip-bomb). Dans la pratique on peut le tester avec moins de layers.

### Chemin de fichier

On peut uploader un .zip contenant un fichier nommé "../index.php" pour écraser le vrai index.php. Voir [evilarc](https://github.com/ptoomey3/evilarc)

## Références
- [Zip bomb](https://github.com/AbhiAgarwal/notes/wiki/Zip-bomb)
- [evilarc](https://github.com/ptoomey3/evilarc)
