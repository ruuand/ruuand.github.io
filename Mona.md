---
title: Mona
permalink: /Mona/
---

Mona est un plugin pour Immunity Debugger et permet de faciliter le développement d'exploits.

Généralités
-----------

Lister les modules avec mona

``` bash
!mona modules
```

Recherche de gadgets
--------------------

Trouver un opcode dans *slmfc.dll* avec Mona:

``` bash
!mona find -s "\xff\xe4" -m slmfc.dll
```

Trouver des *jmp esp* dans user32.dll:

``` bash
!mona jmp -r esp -m user32.dll
```

[Category:Exploitation](/Category:Exploitation "wikilink") [Category:Outils](/Category:Outils "wikilink")