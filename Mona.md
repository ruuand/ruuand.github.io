---
title: Mona
permalink: /Mona/
---

# Mona

Mona est un plugin pour Immunity Debugger et permet de faciliter le développement d'exploits.

## Généralités

Lister les modules avec mona

``` bash
!mona modules
```

Créer un "working folder"

``` basg
!mona config -set workingfolder c:\mona\%p # %p correspond au nom de l'exe courant
```

## Recherche de gadgets

Trouver un opcode dans *slmfc.dll* avec Mona:

``` bash
!mona find -s "\xff\xe4" -m slmfc.dll
```

Trouver des *jmp esp* dans user32.dll:

``` bash
!mona jmp -r esp -m user32.dll
```

## Recherche de bad chars

Créer des fichiers contenant des bytearray (bytearray.bin et bytearray.txt).
``` bash
!mona bytearray # Tous les caractères
!mona bytearray -cpb "\x00\x0a" # Tous sauf \x00 \x0a
```

Comparer le contenu d'un fichier avec ce qu'il y a en mémoire à l'adresse XXXX
``` bash
!mona compare -f C:/mona/minishare/bytearray.bin -a 01010101 
```
