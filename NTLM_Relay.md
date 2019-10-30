---
title: NTLM Relay
permalink: /NTLM_Relay/
---

# NTLM Relay

Cet article tente de présenter les attaques de type "Relai NTLM". Le principe de base de ce type d'attaque est:
1) Forcer un utilisateur à effectuer une connexion sur la machine de l'attaquant
2) Tenter d'accéder à un service cible
3) Relayer l'authentification pour le service cible auprès de la victime
4) PROFIT !

## Récupérer des connexions

Il existe de nombreuses méthodes pour forcer une connexion vers la machine attaquante. Voir l'article [Places of Interest in Stealing NetNTLM Hashes](https://osandamalith.com/2017/03/24/places-of-interest-in-stealing-netntlm-hashes/).

Certains scénarios pratiques sont:
- Man in the middle (Responder)
- Base de donnée MS SQL (avec xp_dirtree)
- Ajouter un fichier (.lnk) sur un partage

## Serveur cible

Il est nécessaire de prendre en compte le serveur cible (machine de la victime ou machine tierce) et le service cible. Dans le cas du serveur cible:
- S'il s'agit de la machine de la victime alors ce n'est normalement pas possible. Faire un "reflective relay" de SMB vers SMB n'est pas possible à cause de MS08-067 et faire un relai "cross-protocol" ne semble pas possible sur les machines récentes (https://github.com/SecureAuthCorp/impacket/issues/451).
- Pour une machine tierce pas de problème spécifique. Le fonctionnement va dépendre du service.

## Service cible

On cherchera généralement à relayer vers SMB, LDAP ou LDAPS. Dans des cas plus spécifiques on pourrait vouloir relayer vers du MS-SQL (pour faire du xp_cmdshell ou xp_dirtree) ou vers du HTTP. Il est cependant nécessaire de prendre en compte le type de connexion effectué par l'utilisateur. Les deux cas les plus courants seront SMB ou HTTP.

### Connexion sur SMB

Si l'utilisateur vient se connecter en SMB on sera limité à du relay SMB -> SMB. Ceci permet de:
- **Prendre le contrôle d'un machine si l'utilisateur est Administrateur local**
- Accéder à un partage réseau

Il n'est pas possible de relayer vers un Active Directory en raison du **SMB Signing**.

### Connexion sur HTTP

Si l'utilisateur vient se connecter en HTTP on pourra faire du relai vers d'autres protocoles (SMB, LDAP, LDAPS, IMAP, MS SQL)

