---
title: DNS Rebinding
permalink: /DNS_Rebinding/
---

# DNS Rebinding

## Principe

DNS Rebinding consiste à faire changer l'adresse IP associée à attacker.com pour la faire passer à une adresse IP correspondant à l'application ciblée. Un navigateur sur attacker.com effectuera des requêtes vers cette cible en pensant qu'il s'agit légitimement de attacker.com.

Une application est vulnérable à l'attaque DNS Rebinding s'il est possible d'y accéder en modifiant le champ "Host:" et en le remplacant par une valeur arbitraire. Cette attaque permet de bypasser la [Same Origin Policy](/SOP/). 

L'attaque a cependant des limites:
- **Validation du Host**: Si le champ "Host" est validé alors l'attaque ne fonctionne pas
- **Authentification**: On ne peut pas accéder à du contenu nécessitant une authentification (le champ Host étant changé les cookies ne seront pas envoyés).
- **HTTPS**: Si HTTPS est utilisé l'attaque échouera. L'application cible ayant un certificat TLS ne matchant pas le domaine attacker.com

De ce fait l'attaque est intéressante pour cibler des applications accessibles uniquement en réseau interne ou en local (ex: transmission).

## Références
### Outils
- [rbndr](https://github.com/taviso/rbndr): service pour tester des attaques de type "Rebinding DNS"

### Articles
- [Walking Past Same-origin Policy, NAT, and Firewall for Ethereum Wallet Control](https://medium.com/@rhodey/walking-past-same-origin-policy-nat-and-firewall-for-ethereum-wallet-control-30c29b73a057)
- [Attacking Private Networks from the Internet with DNS Rebinding](https://medium.com/@brannondorsey/attacking-private-networks-from-the-internet-with-dns-rebinding-ea7098a2d325)
- [CVE-2018-5702 in transmission](https://github.com/transmission/transmission/pull/468)
