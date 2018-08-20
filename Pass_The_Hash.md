---
title: Pass The Hash
permalink: /Pass_The_Hash/
---

# Pass the Hash

La méthode **Pass The Hash** consiste à utiliser le hash NTLM d'un utilisateur pour s'authentifier auprès d'un service. Cette attaque permet de s'authentifier sans connaître le mot de passe en clair. Elle est notamment très utile dans les phases de déplcament latéral.

Utilisation
-----------

Il est nécessaire d'avoir récupéré les informations suivantes:

-   Le nom de l'utilisateur.
-   Le domaine auquel il appartient (sauf s'il s'agit d'un utilisateur local).
-   Le [hash NTLM](/NTLM/) du mot de passe de l'utilisateur.

Avec ces éléments il est alors possible d'executer des commandes sur différents serveurs via le protocole [SMB](/SMB "wikilink").

Mitigation
----------

Voir [Mitigating Pass the Hash Attacks and Other Credential Theft Version 2](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating-Pass-the-Hash-Attacks-and-Other-Credential-Theft-Version-2.pdf)


## Références
-   [Pass The Hash with Kerberos](/https://malicious.link/post/2018/pass-the-hash-with-kerberos/): il est possible de faire une attaque de type pass the hash via Kerberos
