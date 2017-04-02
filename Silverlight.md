---
title: Microsoft Silverlight
permalink: /Silverlight/
---

# Microsoft Silverlight
Microsoft Silverlight permet de gérer des applications qui tournent sur le navigateur client (de manière similaire à du flash ou une applet Java).

## Outils
Quelques outils utiles pour pentester des applications utilisant Silverlight côté client:
* dnSpy: pour décompiler l'executable Silverlight
* [WCF Binary Helper](https://gist.github.com/sekhmetn/4420532) est un plugin Burp qui permet de décoder les échanges basés sur soap+msbin1. Il faut également télécharger NBFS.exe (disponible sur https://github.com/GDSSecurity/WCF-Binary-SOAP-Plug-In/tree/master/burp_pro_wcf_plugin).
** A noter que le plugin n'accepte à priori pas d'envoyer des requêtes ne respectant pas le format soap+msbin1.

## Trucs
* Checker le fichier clientaccesspolicy.xml qui permet de gérer la cross-domain policy avec Microsoft Silverlight.
