---
title: Web Cache
permalink: /Web_Cache/
---

# Web Cache

## Généralites

Les caches web permettent d'accélérer la vitesse de chargement des pages et d'alléger les opérations côté serveur en sauvegardant certaines ressources dans un cache, plus proche de l'utilisateur. Ceci concerne généralement des ressources statiques (images, CSS, etc.)

## Web Cache Deception Attack

Les conditions suivantes sont nécessaires:
- http://www.example.com/home.php/non-existent.css et http://www.example.com/home.php sont identiques. Ceci se produit souvent quand on utilise des patterns d'URLs. On peut s'en protéger avec des patterns de la forme ^page$
- Aucun Cache-Control n'est en place ou le serveur de Cache l'ignore.

La page contient des informations sensibles. Cependant elle peut être mise en cache par un proxy si l'utilisateur y accéde via http://www.example.com/home.php/non-existent.css en raison de l'extension finale. La page apparaît comme le fichier non-existent.css du répertoire home.php.


### Références

- [Web Cache Deception Attack](https://omergil.blogspot.fr/2017/02/web-cache-deception-attack.html)
- [Web Cache Deception Attack WhitePaper](https://www.blackhat.com/docs/us-17/wednesday/us-17-Gil-Web-Cache-Deception-Attack-wp.pdf)
- [Web Cache Deception Scanner (Burp)](https://portswigger.net/bappstore/7c1ca94a61474d9e897d307c858d52f0)

## Références
- [Practical Web Cache Poisoning](https://portswigger.net/blog/practical-web-cache-poisoning)
- [Cracking the lens: targeting HTTP's hidden attack-surface](https://portswigger.net/blog/cracking-the-lens-targeting-https-hidden-attack-surface): l'article présente un exemple d'exploitation sur le cache dans la dernière partie.
