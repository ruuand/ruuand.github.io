---
title: Just Enough Administration
permalink: /Just_Enough_Administration/
---

# Just Enough Administration

Just Enough Administration (JEA) est introduit dans Windows Server 2016 et Windows 10. Cela permet de définir un subset de commandes powershell qui permettent de faire des opérations administratives (redémarrer un service, ajouter un utilisateur, etc.) sans être administrateur local.

Cela reste contraignant à mettre en place car il est nécessaire d'identifier exactement ce qui est nécessaire pour les utilisateurs.

## Contournement

Cette section décrit des mauvaises pratiques sur l'utilisation de JEA qui rendent caduque la protection apportée.
-   JEA n'impose des restrictions que sur Powershell Remoting (?), si un service psexec peut être lancé ou si un RDP est utilisable alors l'attaquant pourra utiliser les credentials qu'il posséde sur ces services
-   Certaines commandes autorisées peuvent être dangereuses
-   Le "Language Mode": ne pas utiliser le "ConstrainedLanguageMode" qui permet de créer de nouvelles fonctions qui peuvent être lancées. Le mode à utiliser est le "NoLanguageMode"
-   Fonctions vulnérables: on peut avoir des injections de commandes 

Ressources
----------

-   [Just Enough Administration Overview](https://msdn.microsoft.com/powershell/jea/overview)
-   [Reduce the number of admins on your servers with Just Enough Administration](https://blogs.technet.microsoft.com/datacentersecurity/2016/08/29/jea-overview/)
-   [DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server](https://www.youtube.com/watch?v=ahxMOAAani8)
