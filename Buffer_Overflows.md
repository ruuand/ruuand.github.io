---
title: Buffer Overflows
permalink: /Buffer_Overflows/
---

# Buffer Overflows

## Généralités

Cette section contient des commandes générales utiles pour l'exploitation de buffer overflows.

Générer des patterns avec metasploit:

``` bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb 2700 # Génération du pattern
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb 39694438 # Trouver l'offset
```

Trouver un jmp avec mona dans un module spécifique:

``` bash
!mona jmp -!mona jmp -r esp -m user32.dll
```

### Bad characters

Pour rechercher des bad chars on peut générer un payload avec mona:

``` bash
!mona bytearray # Tous les caractères
!mona bytearray -cpb "\x00\x0a" # Tous sauf \x00 \x0a
```

On peut comparer un fichier avec le contenu en mémoire:

``` bash
!mona compare -f C:/mona/minishare/bytearray.bin -a 01010101 
```

Cette chaîne peut être utilisée pour chercher les "**bad chars**":

``` text
buf="\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10"
buf+="\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20"
buf+="\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30"
buf+="\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40"
buf+="\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50"
buf+="\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60"
buf+="\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70"
buf+="\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80"
buf+="\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90"
buf+="\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0"
buf+="\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0"
buf+="\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0"
buf+="\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0"
buf+="\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0"
buf+="\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0"
buf+="\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff"
```

Il faut également s'assurer que les bad chars n'empêchent pas le crash pour pouvoir facilement trouver à quel char on s'est arrêté.

### Générer shellcodes

On peut utiliser metasploit pour trouver les équivalents opcode de certaines instructions:

``` text
# /usr/share/metasploit-framework/tools/exploit/nasm_shell.rb
nasm > jmp esp
00000000  FFE4              jmp esp
```

## SEH Overflows

Les commandes mona suivantes permettent l'exploitation :
``` bash
!mona exchain # Affiche les enregistrements SEH (on peut aussi faire ALT+S)
!mona safeseh # Affiche les modules sans SafeSEH
!mona seh -m strmdll.dll # Chercher un pop,pop,ret dans le module indiqué
```

Il faut trouver un payload de la forme suivante:
``` bash
[JUNK][Short JMP          ][Address to POP, POP, RET][NOPs][Shellcode]
[????][Address to next SEH][Address of SEH Handler  ][???????????????]
```

Si on utilise msfvenom il faut préciser EXITFUNC=SEH.

## Unicode

msfvenom dispose d'un encoder pour générer des payloads compatibles avec de l'unicode:

``` bash
msfvenom -p windows/exec -e x86/unicode_mixed CMD=calc.exe BufferRegister=eax --format=py
```

Il est cependant nécessaire d'initialiser la valeur de registre eax pour qu'elle pointe vers le début du buffer. FuzzySecurity montre une démarche (voir détail complet dans le [tutorial](http://www.fuzzysecurity.com/tutorials/expDev/5.html)). 

## Return Oriented Programming (ROP)

Les commandes mona suivantes sont utiles pour les exploits ROP:

``` bash
!mona modules # Liste les informations sur les différents modules
!mona ropfunc -m MSRMfilter03.dll -cpb '\x00\x09\x0a' # Liste les fonctions utiles pour ROP dans MSRMfilter03.dll (VirtualAlloc, etc.)
!mona rop -m MSRMfilter03.dll -cpb '\x00\x09\x0a' # Liste les gadgets dans MSRMfilter03.dll. Cette commande génère plusieurs fichiers. Le fichier rop_chains.txt contient la structure (valeurs à mettre dans les registres, etc.) pour faire un exploit valide.
```

## Contournement de protections

### Stack Cookies

Méthodes de contournement:
- Cookie prévisible (statique, faible entropie, etc.)
- Attaque SEH

### Data Execution Prevention (DEP)

Méthodes de contournement:
- Return Oriented Programming
- Return to LIBC

### Address Space Layout Randomization (ASLR)

Méthodes de contournement:
- Partial EIP Overwrite (voir [tutorial Corelan](https://www.corelan.be/index.php/2009/09/21/exploit-writing-tutorial-part-6-bypassing-stack-cookies-safeseh-hw-dep-and-aslr/))

## Ressources

### Liens externes

- [64 Bits Linux Stack Based Buffer Overflow](https://www.exploit-db.com/docs/33698.pdf)
- [Windows Exploit Development - Part 1](http://www.shogunlab.com/blog/2017/08/19/zdzg-windows-exploit-1.html)
- [Tutorials Fuzzy Security](http://www.fuzzysecurity.com/tutorials.html)
