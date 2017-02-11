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

Voir <https://download.microsoft.com/download/7/7/a/77abc5bd-8320-41af-863c-6ecfb10cb4b9/mitigating%20pass-the-hash%20(pth)%20attacks%20and%20other%20credential%20theft%20techniques_english.pdf>
