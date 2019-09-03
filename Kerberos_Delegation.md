---
title: Kerberos Delegation
permalink: /Kerberos_Delegation/
---

# Kerberos Delegation

La délégation [Kerberos](/Kerberos/) permet à un service A d'accéder à un service B en se faisant passer pour un utilisateur. L'utilisateur "délégue" ses droits au service A.

## Unconstrained Delegation

Ce type de délégation était le premier et il est toujours présent pour des raisons de rétro-compatibilité. Dans ce mode, l'utilisateur fournit un TGS au service A mais ce TGS contient un TGT pour l'utilisateur. Le service A peut alors utiliser ce TGT pour accéder au service B. Dans la pratique ceci lui permet d'accéder à n'importe quel service en se faisant passer pour l'utilisateur.

Quelques notes:
- L'unconstrained delegation est configurée au niveau d'un serveur. Ainsi un utilisateur accédant à n'importe quel service de ce serveur enverrait son TGT.
- Par défaut tous les contrôleurs de domaine ont l'Unconstrained Delegation.
- Si l'utilisateur est dans le groupe "Protected Users" ou s'il a l'option "Account is sensitive and cannot be delegated" alors il n'enverra pas de TGT dans le TGS.
- Une attaque utilisant [MS-RPRN](/MS_RPRN/) utilise ce défaut. Elle permet notamment prendre le contrôle d'une autre forêt.

## Constrained Delegation - Traditional (Windows 2003)

Dans sa version classique la "Constrained Delegation" se configure au niveau d'un compte (utilisateur ou ordinateur) via l'attribut **msDS-AllowedToDelegateTo**. Cet attribut contient une liste de services pour lesquels le compte peut se faire passer pour n'importe quel utilisateur.

Le mécanisme se base sur deux extensions S4U2self (Server for user) et S4U2proxy.:
- S4Uself: le service peut demander un ticket pour lui-même comme s'il était l'utilisateur. Ce ticket est "forwardable". Il peut faire cette opération pour n'importe quel utilisateur !
- S4Uproxy: le service utilise un ticket forwardable pour accéder au service voulu. Le DC valide que le service voulu est bien dans la liste **msDS-AllowedToDelegateTo** et renvoie un TGS avec les droits de l'utilisateur.

Il y a ensuite deux possibilités:
- **Constrained Delegation**: dans ce cas c'est l'utilisateur qui demande un ticket forwardable et le fournit ensuite au service qui s'en sert avec S4U2Proxy
- **Constrained Delegation with protocol transition**: dans ce cas c'est le service A qui demande un ticket en se faisant passer pour l'utilisateur (S4U2Self) et s'en sert ensuite avec S4U2Proxy

Quelques notes:
- Le userAccountControl doit contenir TRUSTED_TO_AUTH_FOR_DELEGATION pour que le compte puisse faire de la délégation. Dans la pratique si ce flag n'est pas set alors le compte ne peut pas récupérer un ticket Forwardable, cependant il peut récupérer un ticket non-forwardable qui peut être utiliser dans le cadre de Ressource-Based Constrained Delegation.
- Le service name contenu dans msDS-AllowedToDelegateTo n'est pas important, ce qui compte c'est le serveur indiqué (voir [Kerberos Delegation SPNs and more](https://www.secureauth.com/blog/kerberos-delegation-spns-and-more))
- Un privilége spécifique (SeEnableDelegationPrivilege) est nécessaire pour modifier l'attribut **msDS-AllowedToDelegateTo**.
- Ce mécanisme ne nécessite pas que l'utilisateur s'authentifie auprès du serveur !
- Si un DC est dans la liste on peut faire du DCSync.
- Comme pour Unconstrained Delegation, les Protected Users et "Account is sensitive" ne peuvent pas être ciblés.

Plus d'infos [S4U2Pwnage](https://www.harmj0y.net/blog/activedirectory/s4u2pwnage/)

## Resource-based Constrained Delegation (Windows 2012)

Dans cette version, c'est le service final (service B) qui indique quels utilisateurs ou ordinateurs sont autorisés à effectuer de la délégation via le champ **msDS-AllowedToDelegateTo**.

Quelques notes:
- Le champ **msDS-AllowedToDelegateTo** peut être édité sans SeEnableDelegationPrivilege.
- Attaque: Un attaquant qui contrôle un compte avec TRUSTED_TO_AUTH_FOR_DELEGATION et qui peut éditer le champ **msDS-AllowedToDelegateTo** peut alors se faire passer pour n'importe quel utilisateur auprès de ce service en ajoutant le compte avec TRUSTED_TO_AUTH_FOR_DELEGATION dans **msDS-AllowedToDelegateTo**.
- Dans ce mode le ticket reçu par service B n'a pas besoin d'être forwardable. Ainsi un attaquant parvenant un récupérer un TGS pour service A peut l'utiliser. Dans ce cas l'attaquant peut se faire passer pour l'utilisateur auprès du service B (à condition qu'il puisse ajouter service A dans le **msDS-AllowedToDelegateTo** de service B).

## Références

### Articles

- [Another word on delegation](https://www.harmj0y.net/blog/redteaming/another-word-on-delegation/)
- [Kerberos Delegation SPNs and more](https://www.secureauth.com/blog/kerberos-delegation-spns-and-more)
- [S4U2Pwnage](https://www.harmj0y.net/blog/activedirectory/s4u2pwnage/)
- [From Kekeo to Rubeus](http://www.harmj0y.net/blog/redteaming/from-kekeo-to-rubeus/)
- [Wagging the dog](https://shenaniganslabs.io/2019/01/28/Wagging-the-Dog.html)
- [The worst of both worlds: Combining NTLM Relaying and Kerberos delegation](https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/)
- [Delegating like a Boss: Abusing Kerberos Delegation in Active Directory](https://horizon.guidepointsecurity.com/tutorials/delegating-like-a-boss-abusing-kerberos-delegation-in-active-directory/)
- [Gone to the Dogs (élévation de privilèges)](https://shenaniganslabs.io/2019/08/08/Lock-Screen-LPE.html). La même attaque est décrite dans l'article suivant [Kerberos Resource-Based Constrained Delegation: When an Image Change Leads to a Privilege Escalation
](https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2019/august/kerberos-resource-based-constrained-delegation-when-an-image-change-leads-to-a-privilege-escalation/)

### Interne

- [Kerberos](/Kerberos/)
