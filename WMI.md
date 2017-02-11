---
title: WMI
permalink: /WMI/
---

# WMI

WMI permet d'executer des commandes à distance (à la manière de [PsExec](/PsExec "wikilink")). Cependant son utilisation est plus discréte.

Commandes utiles
----------------

Impacket propose un executable wmiexec.py:

``` python
wmiexec.py -hashes aad3b435b51404eeaad3b435b51404ee:aad3b435b51404eeaad3b435b51404ee Administrateur@172.0.0.1
```

Metasploit ne propose pas de module permettant de déployer directement un meterpreter avec WMI. Il existe cependant un module **web_delivery** qui permet de déployer un meterpreter via un serveur web local, metasploit fournit alors une ligne de commande qui peut être copiée/collée dans wmiexec.

Référence
---------

-   [We Don’t Need No Stinkin’ PSExec](https://www.trustedsec.com/june-2015/no_psexec_needed/)
-   [Executing code via SMB / DCOM without PSEXEC](https://room362.com/post/2014/2014-04-19-executing-code-via-smb-without-psexec/)

[Category:Technologies](/Category:Technologies "wikilink")
