---
title: MsCacheV2
permalink: /MsCacheV2/
---

# MsCacheV2

Par défaut Windows stocke des hashs des utilisateurs du domaine qui s'authentifient pour permettre une authentification quand le DC n'est pas joignable.

Mimikatz permet de dumper ces hashs:
```
meterpreter > kiwi_cmd lsadump::cache
```
Le nombre de credentials gardé en cache est contrôlé par une clé de registre:

``` text
   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\Current Version\Winlogon\

   ValueName: CachedLogonsCount
   Data Type: REG_SZ
   Values: 0 - 50
```

Quelques éléments importants:
- MsCacheV2 est salé avec le nom de l'utilisateur
- MsCacheV2 utilise RC4 avant Vista & 2008. A partir de ces versions il utilise PBKDF2 avec 1024 itérations. A noter que le nombre d'itérations peut être différent (voir [MsCache v2 / DCC2 et nombre d’itérations](http://blog.gentilkiwi.com/securite/mscache-v2-dcc2-iteration))
- Il est possible d'empêcher le système de conserver un hash en local (surtout sur les serveurs)
- Mettre une valeur de "1" pour CachedLogonsCount peut avoir des effets de bord indésirables (voir [Cached logons and CachedLogonsCount](https://blogs.technet.microsoft.com/instan/2011/12/06/cached-logons-and-cachedlogonscount/))

## Références
- [Cached domain logon information](https://support.microsoft.com/en-us/kb/172931)
