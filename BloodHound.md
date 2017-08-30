---
title: BloodHound
permalink: /BloodHound/
---

# BloodHound

## Utilisation

Il faut importer le module. **Note:** il y a une erreur si Powersploit a déjà été importé:

``` powershell
Import-Module .\BloodHound.ps1
```

Puis lancer la récupération des informations

``` powershell
Get-BloodHoundData | Export-BloodHoundCSV
```

Puis on importe dans BloodHound. The end.

## Hardening

Il est possible d'empêcher l'énumération des sessions locales avec l'outil [NetCease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)

## Ressources

-   [Projet Github](https://github.com/adaptivethreat/BloodHound)
-   [BloodHound - Custom Queries](http://www.securityripcord.com/blog/2016/09/28/bloodhound-custom-queries/)
-   [Extending BloodHound: Track and Visualize Your Compromise](http://porterhau5.com/blog/extending-bloodhound-track-and-visualize-your-compromise/)
-   [The ACL Attack Path Update](https://wald0.com/?p=112)
