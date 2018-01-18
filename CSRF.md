---
title: Cross-Site Request Forgery
permalink: /CSRF/
---

# Cross-Site Request Forgery

## Exploitation

Dans certains cas il peut être compliqué d'exploiter un CSRF, notamment s'il faut ajouter un en-tête spécifique ou si le payload doit être en JSON. Il existe cependant des méthodes basées sur des applets Flash (voir [Exploiting JSON Cross Site Request Forgery (CSRF) using Flash](https://www.geekboy.ninja/blog/exploiting-json-cross-site-request-forgery-csrf-using-flash/))

## Points de contrôles

Les points suivants sont à vérifier:

- Présence de token (ou validation avec mot de passe)
- Aléas du token
- Renouvellement du token ? Chaque requête (idéal) ou chaque session ?
- Divulgation du token (regarder les éléments .json ou .js qui pourraient le contenir. Ex: [Badoo CSRF](https://hackerone.com/reports/127703))

## Références
- [Exploiting JSON Cross Site Request Forgery (CSRF) using Flash](https://www.geekboy.ninja/blog/exploiting-json-cross-site-request-forgery-csrf-using-flash/))
