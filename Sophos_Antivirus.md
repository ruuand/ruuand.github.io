---
title: Sophos Antivirus
permalink: /Sophos_Antivirus/
---

# Sophos Antivirus

Mise à jour
-----------
Sophos Antivirus utilise un compte pour se connecter au serveur local pour les mises à jours. Ce compte peut être un compte du domaine. Les informations sur le compte (nom, mot de passe chiffré et serveur de mise à jour).

- Il est possible de récupérer un challenge NetNTLMv1/v2 en se faisant passer pour le serveur de mise à jour (avec [Responder](/Responder/) par exemple)
- Il est possible de récupérer le mot de passe en mémoire (avec [Mimikatz](/Mimikatz/)) au moment de déclencher la mise à jour.

Références
----------
- [User accounts required by Sophos Enterprise Console](https://community.sophos.com/kb/en-us/113954)
- [Sophos Anti-Virus updater password decoder](https://github.com/aurainfosec/sophos-pw-decoder)
