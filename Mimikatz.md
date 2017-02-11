---
title: Mimikatz
permalink: /Mimikatz/
---

# Mimikatz

Conditions
----------

Pour utiliser mimikatz il faut pouvoir le lancer en tant qu'administrateur ou SYSTEM. Ensuite on peut récupérer des informations, modulo certaines conditions.

Les hashs LM (et mdp) sont stockés dans certaines conditions (source: <http://www.ampliasecurity.com/research/wce12_uba_ampliasecurity_eng.pdf> & <https://technet.microsoft.com/en-us/library/hh994565(v=ws.11).aspx>):

-   Interactive logon sessions at the console
-   Remote logon sessions via RDP
-   RunAs
-   Windows Services running under specific user accounts
-   Windows APIs used by applications
-   Etc

Défenses
--------

Il existe plusieurs mécanismes pour se défendre contre les attaques utilisant Mimikatz (Plus d'informations sur ADSecurity: <https://adsecurity.org/?p=559>)

### Désactiver wdigest

A partir de Windows 8.1 et Windows Server 2012 les mots de passes ne sont plus stockés en mémoire par défaut. De plus il est possible de faire en sorte que les mots de passe n'apparaissent pas en mémoire dans les anciennes versions de Windows. Il faut pour cela:

-   Appliquer le patch KB2871997
-   Modifier la clé de registre suivante pour qu'elle ait 0:

``` text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest “UseLogonCredential”(DWORD)
```

Commandes
---------

Pour lancer powershell en tant que SHINRA-INC\\heidegger (y compris sur une machine qui n'est pas liée au domaine).

``` bash
privilege::debug
sekurlsa::pth /user:heidegger /domain:SHINRA-INC /ntlm:XXXXXXXXXXXXXXXX /run:powershell.exe
```

Références
----------

-   [Unofficial Guide to Mimikatz & Command Reference - ADSecurity](https://adsecurity.org/?page_id=1821)
-   [Mimikatz Overview, Defenses and Detection](https://www.sans.org/reading-room/whitepapers/detection/mimikatz-overview-defenses-detection-36780)
-   [Utilisation avancée de Mimikatz](http://connect.ed-diamond.com/MISC/MISC-066/Utilisation-avancee-de-Mimikatz)

[Category:Outils](/Category:Outils "wikilink")
