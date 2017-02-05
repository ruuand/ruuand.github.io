---
title: BloodHound
permalink: /BloodHound/
---

Utilisation
-----------

Il faut importer le module (**Note:** il y a une erreur si Powersploit a déjà été importé):

``` powershell
Import-Module .\BloodHound.ps1
```

Puis lancer la récupération des informations

``` powershell
Get-BloodHoundData | Export-BloodHoundCSV
```

Puis on importe dans BloodHound. The end.

Ressources
----------

-   [Projet Github](https://github.com/adaptivethreat/BloodHound)
-   [BloodHound - Custom Queries](http://www.securityripcord.com/blog/2016/09/28/bloodhound-custom-queries/)

[Category:Outils](/Category:Outils "wikilink")