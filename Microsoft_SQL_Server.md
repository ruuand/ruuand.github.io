---
title: Microsoft SQL Server
permalink: /Microsoft_SQL_Server/
---

# Microsoft SQL Server

## Utilisation
### Connexion

Impacket posséde un outil *mssqlclient.py*. L'exemple suivant permet de se connecter avec sa/password et d'executer les commandes contenues dans *commands.txt*:

``` bash
mssqlclient.py -port 27900 sa:password@192.168.31.227 -file commands.txt
```

## Checklist
Eléments à tester pour Microsoft SQL server:
- Mots de passes par défaut (sa/sa, sa/null) ou faibles (Metasploit, Nessus)
- Connexion avec comptes du domaines (Metasploit)
- Enumération des bases de données via SPN (PowerUpSQL)
- Avec un compte administrateur:
    - xp_cmdshell
- Avec un compte à priviléges limités:
    - xp_dirtree ou xp_filexist pour faire du SMB Relay (si le compte BDD est intéressant)
    - Elevation de priviléges (Voir PowerUpSQL)

## Ressources

### Vidéos

- [Hacking SQL Servers on Scale using PowerShell](https://www.youtube.com/watch?v=npoORzfP7rw&feature=youtu.be)

### Outils

- [PowerUpSQL](https://github.com/NetSPI/PowerUpSQL)
- [SQL Server Link Crawling with PowerUpSQL](https://blog.netspi.com/sql-server-link-crawling-powerupsql/)
