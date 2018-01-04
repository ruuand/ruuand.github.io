---
title: Google Web Toolkit
permalink: /GWT/
---

# Google Web Toolkit (GWT)

GWT est un framework permettant de faire des applications web. Il permet une réutilisation du code côté client & serveur. Il va générer du code Javascript pour la partie cliente en cherchant à l'optimiser pour les différents navigateurs.

## Fonctionnement global

- Le navigateur télécharge app.nocache.js puis EDE39CE15AF13C74473DA6EBD45DB656.cache.html (dépend du browser)
- Le code côté client est obfusqué
- Le protocole GWT-RPC est utilisé pour la communication client serveur. Il s'agit d'une forme de serialisation.
- Les réponses sont sérialisées avec du JSON.

## Références

### Outils
- [GWT-Penetration-Testing-Toolset](https://github.com/GDSSecurity/GWT-Penetration-Testing-Toolset)

### Articles
- [GWT Web App Hacking](http://www.h0wl.pl/2012/03/gwt-web-app-hacking.html)
- [Unlocking the Toolkit: Attacking Google Web Toolkit with Ron Gutierrez](https://vimeo.com/20437969)
- [From Serialized to Shell :: Auditing Google Web Toolkit](https://srcincite.io/blog/2017/04/27/from-serialized-to-shell-auditing-google-web-toolkit.html)
