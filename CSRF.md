---
title: Cross-Site Request Forgery
permalink: /CSRF/
---

# Cross-Site Request Forgery

## Points de contrôles

Les points suivants sont à vérifier:

- Présence de token (ou validation avec mot de passe)
- Aléas du token
- Renouvellement du token ? Chaque requête (idéal) ou chaque session ?
- Divulgation du token (regarder le éléments .json ou .js qui pourraient le contenir)
