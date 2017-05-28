---
title: Assembleur
permalink: /Assembleur/
---

# Assembleur

Cet article présente différentes informations concernant le langage assembleur (ASM).

Outils
------

Les outils suivants sont utiles:

-   nasm
-   ld
-   gdb

### nasm

Documentation: <http://www.nasm.us/doc/>

$ représente l'addresse "courante

``` asm
    label: db "Hello World" ; define byte
    len    equ  $-label   ; contient la longueur de label qui est $ (adresse courante) - label (adresse du début de la chaîne)
```

Génération d'executable
-----------------------

Pour générer un executable à partir de code ASM:

``` bash
nasm -f elf32 -o test.o test.asm # Assembling
ld -melf_i386 -o test test.o # Linking
```

Code ASM
--------

### Instructions classiques

Quelqus instructions classiques:

``` asm
mov eax, 0x01 ; met 1 dans eax
lea eax, [label] ; charge un pointeur vers label dans eax ( a revoir)
xchg reg1, reg2 ; échange les valeurs entre deux registres / pointeurs
```

### System calls

On peut les trouver à /usr/include/x86_64-linux-gnu/asm/unistd_32.h

On peut avoir leur doc en faisant:

``` bash
man 2 write
man 2 exit
[...]
```

Quand on fait un syscall:

-   EAX contient le sytem call number et contiendra la valeur de retour
-   EBX, ECX, EDX, ESI, EDI contiennent les arguments (il y a des alternatives avec des structures, notamment quand on a plus d'arguments)

### Exemple de code ASM

Ceci est un exemple basique de code ASM:

``` asm
; Commentaire

global _start

section .text ; contient le code assembleur

_start:
    ; syscall pour printer "Hello World"
    mov eax, 0x4    ; syscall 4 pour "write"
    mov ebx, 0x1    ; 1 pour stdout
    mov ecx, label
    mov edx, len    ; longueur
    int 0x80        ; effectue le syscall

    ; syscall pour faire un exit
    mov eax, 0x1    ; syscall 1 pour "exit"
    mov ebx, 0x3    ; renvoie 3 en sortie
    int 0x80

section .data ; contient des valeurs statiques comme des chaînes des strings
    label: db "Hello World" ; define byte
    len    equ  $-label   ; contient la longueur de label
```

## Références
- [https://azeria-labs.com/writing-arm-assembly-part-1/](Introduction to ARM Assembly basics)
- [https://github.com/Billy-Ellis/Exploit-Challenges}(Exploit challenges)
