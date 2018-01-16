---
title: DNS Rebinding
permalink: /DNS_Rebinding/
---

# DNS Rebinding

## Exploitation

Une application est vulnérable à l'attaque DNS Rebinding s'il est possible d'y accéder en modifiant le champ "Host:" et en le remplacant par une valeur arbitraire.

## Références
### Outils
- [rbndr](https://github.com/taviso/rbndr): service pour tester des attaques de type "Rebinding DNS"

### Articles
- [Walking Past Same-origin Policy, NAT, and Firewall for Ethereum Wallet Control](https://medium.com/@rhodey/walking-past-same-origin-policy-nat-and-firewall-for-ethereum-wallet-control-30c29b73a057)
- [CVE-2018-5702 in transmission](https://github.com/transmission/transmission/pull/468)
