---
title: Bash
permalink: /Bash/
---

# Bash

Commandes utiles
----------------

Les commandes suivantes permettent de compter le nombre de caractères dans un shellcode:

``` bash
cat ms_08_067.py| grep "^shellcode" | awk '{print $3}' | cut -d'"' -f2 | sed ':a;N;$!ba;s/\n//g' | wc -c
```

Faire des divisions sur la CLI:

``` bash
v=$(cat tmp | cut -d'"' -f2 | tr -d '\n' | wc -c);echo $((v/4))
```

Les commandes suivantes générent les commandes à taper pour copier/coller un fichier dans un shell non interactif:

``` bash
cat test | sed -e 's/^/echo /g' | sed -e 's/$/>> file.txt/g'
```

Faire tourner un outil en boucle sur chaque ligne d'un fichier
```
while read dom; do /opt/testssl.sh/testssl.sh --csv $dom ; done < domains.txt
```
