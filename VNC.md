---
title: VNC
permalink: /VNC/
---

# VNC

Prendre un screenshot via VNC:

```
# Le fichier vncpasswd.txt peut être généré avec l'outil vncpasswd
vncsnapshot -passwd vncpasswd.txt 192.168.100.100 out
```

Avec une boucle
```
while read ip; do vncsnapshot -passwd ../vncpasswd.txt $ip screen2_$ip; done < ../vnc.list
```

On peut retrouver le mot de passe VNC dans certaines clés de registre:
```
\HKEY_LOCAL_MACHINE\SOFTWARE\TigerVNC\WinVNC4
\HKEY_LOCAL_MACHINE\SOFTWARE\TightVNC\Server
\HKEY_LOCAL_MACHINE\SOFTWARE\ORL\WinVNC3\Default
\HKEY_LOCAL_MACHINE\SOFTWARE\RealVNC\WinVNC4\
\HKEY_CURRENT_USER\Software\TightVNC
\HKEY_CURRENT_USER\Software\TurboVNC
\HKEY_CURRENT_USER\Software\ORL\WinVNC3\Password
\HKEY_USERS\.DEFAULT\Software\ORL\WinVNC3\Password
```

## Références
* [VNC Security Audit](https://miloserdov.org/?p=4854)
