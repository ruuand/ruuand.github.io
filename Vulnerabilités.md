---
title: Vulnérabilités
permalink: /Vulnerabilités/
---

# Vulnérabilités

Vulnérabilités réseaux
----------------------
- Absence de Network Access Control (NAC) ou contournement possible (MAC Filtering)
- Protocoles potentiellement dangereux: CDP, STP, OSPF, VTP, HSRP (Wireshark)
- Utilisation de LLMNR/NBNS ([Responder](/Responder/))
- Mauvaise segrégation réseau (accès complet aux autres réseaux, LAN unique)
- Absence de protection contre les attaques MitM (e.g. ARP Spoofing)
- Absence de [SMB Signing](/SMB_Relay/) (SMBRelay)
- Service / utilisateur tente de s'authentifier sur la machine de l'attaquant

Active Directory
----------------
- Null session sur serveur / AD
- Politique de mot de passe faible (complexité, renouvellement, blocage de compte)
- Comptes sensibles kerberoastables
- Utilisation de Group Policy Preferences (GPP)
- Mauvaise gestion des comptes administratifs
- Mauvaise configuration des trusts relationships
- Mauvaise gestion des priviléges des comptes (notamment comptes de services)
- MS14-068
- Utilisation de hash LM sur l'AD

Serveur / Poste de travail
--------------------------
- Utilisation de comptes utilisateurs pour l'administration
- Utilisation de hash LM en local
- Stockage de hash MsCacheV2 trop élevé
- Réutilisation du mot de passe d'admin local
- Problèmes de patching
- Pas de restriction sur l'execution (AppLocker ou autre)

# Mails / Internet
- Macros offices autorisées
- PAs de restrictions sur les fichiers executables télécharges en pièce jointe

Partages réseaux & fichiers
---------------------------
- Droits en lecture sur des fichiers sensibles
- Droits en écriture sur des fichiers sensibles / scripts
- Mauvaise configuration des partages réseau (Accès anonyme / Simple utilisateur)
- Mot de passe dans des fichiers en clair

Applications & services
-----------------------
- Présence de services vulnérables
- Mot de passe par défaut (ou faible)
	- Tomcat
	- Jenkins
	- Imprimantes avec compte de domaine
	- mssql
- Communautés SNMP public par défaut
- Communautés SNMP private par défaut
- Accès FTP en anonymous
- Absence de chiffrement des communications (HTTP, FTP, etc.)

Gestion des patchs
------------------
- Patchs de sécurité manquants
	- MS17-010,  MS14-068
- Systèmes obsolétes
	
Réseau Wi-Fi
------------
- Wi-Fi corporate protégé par WPA2
- Wi-Fi corporate protégé par authent machine uniquement
- Wi-Fi corporate protégé par authent AD uniquement

Poste de travail
----------------
- Stockage des hashs LM
- Politique de mot de passe locale
- Absence de chiffrement du poste de travail
- Absence de protection du BIOS
- Absence d'antivirus
- Réutilisation du mot de passe de l'admin local
- Activation de WPAD
- Activation LLMNR
- Activation de NetBIOS
- Activtion de Windows Scripting
- Mot de passe en mémoire (Patch Windows + providers wdigest)
- Possible de s'authentifier en Admin Local (RID 500) ou autre via le réseau
- Déployer AppLocker
- Active Credential Guard & Device Guard (Windows 10)
- LM Authentication -> Sécuriser
- Activer NetCease
- Désactiver SMBv1

[Securing Windows Workstations: Developing a Secure Baseline](https://adsecurity.org/?p=3299)

Serveurs
--------
- Supprimer RC4 HMAC Kerberos (AD W2008)
- Utiliser les "Managed Service Accounts" (AD W2008)
- Utiliser les smart cards (AD W2008)
- Group Managed Service Accounts (AD W2012)
- Kerberos Armoring (AD W2012)
- Authentication Policies & Silos (AD W2012 R2)
- Protected Users Security Group (AD W2012 R2)
- Enable NTLM Auditing
- LM Authentication level: Send NTLMv2 & refuser LM / NTLM (si possible)
- LSASS Auditing
- LSA Protection
- SMB Signing
- Désactiver l'énumération anonyme des shares
- Wdigest
- La plupart des recommendations pour les postes restent valides

Antivirus
---------
- Absence d'antivirus
- Compte de service Antivirus
- Utilisation de NTLMv1

