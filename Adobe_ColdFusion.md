---
title: Adobe ColdFusion
permalink: /Adobe_ColdFusion/
---

Exploitation
------------

### Shell

Avec un accès administateur il est possible d'obtenir un shell sur le serveur. Pour cela il faut utiliser la fonctionnalité *"Debugging & Logging &gt; Code Analyzer"* qui permet de voir les répertoires pour trouver wwwroot.

On peut ensuite uploader avec *"Debugging & Loging / Scheduled Taks"*. Cette fonctionnalité permet de demander à Adobe CF de télécharger un fichier depuis un lien (Il est nécessaire de cocher "Save output to file"). Un webshell four ColdFusion se trouve dans Kali. Pour l'utiliser il faut fournir les valeurs suivantes:

-   Command: C:\\Windows\\System32\\cmd.exe
-   Options: /c dir

Resources
---------

-   [Coldfusion for pentesters](http://www.carnal0wnage.com/papers/LARES-ColdFusion.pdf)
-   [Attacking Adobe Coldfusion](http://jumpespjump.blogspot.fr/2014/03/attacking-adobe-coldfusion.html)

[Category:Technologies](/Category:Technologies "wikilink")