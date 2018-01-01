---
title: Read-Only Domain Controllers
permalink: /RODC/
---

# Read-Only Domain Controllers (RODC)

## Généralités
Quelques éléments généraux sur les RODC:
- Un RODC contient une copie "Read-Only" du DC
- Les credentials (hashs) et d'autres éléments sensibles (clés Bitlocker, LAPS) ne sont pas stockés dans un RODC. Il est possible de configurer le RODC pour avoir un sous-ensemble de ces éléments (ex: hashs des utilisateurs d'un site spécifique)
- Aucune réplication entre RODC. Aucune réplication d'un RODC vers un DC. Réplication possible d'un DC vers un RODC.
- Un RODC a son propre krbtgt (ex: krbtgt_27140)

## Références
- [Attacking Read-Only Domain Controllers (RODCs) to Own Active Directory](https://adsecurity.org/?p=3592)
