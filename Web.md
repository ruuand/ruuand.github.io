---
title: Test d'intrusion Web
permalink: /web/
---

# Test d'intrusion Web

## Reconnaissance

## Headers

- [ ] **X-Frame-Options**
- [ ] **X-XSS-Protection**
- [ ] **Cross Origin Ressource Sharing (CORS)**
- [ ] **Content Security Policy (CSP)**
- [ ] **Strict Transport Security (HSTS)**

## Authentification & gestion de la session

- [ ] **Complexité de mot de passe**
- [ ] **Blocage de compte**: Blocage de compte ? Peut on énumérer des comptes via le blocage ?
- [ ] **Actions sensibles (re-authent)**: Les actions sensibles nécessitent elles une ré-authent (ex: site bancaire)
- [ ] **Renouvellement cookie de session**: Le cookie est il renouvelé après authentification (Session Fixation)
- [ ] **Changement de mot de passe**: Faut il confirmer son ancien mot de passe ?
- [ ] **Oubli de mot de passe**: Envoi d'un lien à usage unique ? Valeur aléatoire du lien ? Ou alors nouveau mot de passe par mail ?
- [ ] **Aléa cookie de session**: Sequencer de Burp. Modifier le cookie pour voir si toutes les parties sont utiles.
- [ ] **Expiration du cookie de session**: réutiliser un cookie obtenu en début de semaine.
- [ ] **Déconnexion**: la session est elle bien invalidée à la déconnexion ?
- [ ] **JSON Web Tokens**
- [ ] **Comptes triviaux**
- [ ] **Enumération des utilisateurs**: formulaire d'authentification, de création de compte, de renouvellement de mot de passe.

## Chiffrement communications

- [ ] **Présence de chiffrement**
- [ ] **Vulnérabilités SSL/TLS**
- [ ] **Certificat**: certificat valide ? Algorithme de signature ?

## Base de données

Si on parvient à lire le contenu de la base de données:

- [ ] **Priviléges utilisateurs BDD**: L'utilisateur BDD est il admin ? Peut il accéder à d'autres bases ?
- [ ] **Mot de passe utilisateur**: En clair ? Chiffrement réversible ? Stockage sous forme de hash ? Algorithme utilisé ? Utilisation d'un sel ?

## Entrées utilisateurs

Les formulaires et l'ensemble des paramètres sont des entrées utilisateurs et peuvent donc être la cible des attaques suivantes:

- [ ] **Command Injection**
- [ ] **[Injection SQL](/SQL_Injection/)**
- [ ] **[XSS (Stored, Reflected, DOM)](/XSS/)**
- [ ] **Open redirect**: à tester quand une redirection a lieu.
- [ ] **Injections XML / LDAP / etc.**
- [ ] **XML External Entity (XXE)**: à tester systématiquement quand on sait que du contenu XML est interprété côté serveur. Notamment dans les cas où on peut uploader des fichiers Word / Excel qui sont des fichiers XML
- [ ] **Path Traversal**
- [ ] **Server Side Request Forgery**

## Formulaire d'upload

- [ ] **Contrôle antivirus**: peut-on uploader un fichier contenant EICAR ? .exe ou autre ?
- [ ] **Contournement des contrôles**: il y a t'il des restrictions ? Peut on les contourner
- [ ] **Accès aux documents**: peut on accéder aux documents uploadés ? (Lien simple, pas d'accès, validation utilisateur, etc.)
- [ ] **Interprétation contenu**: comment est interprété le contenu uploadé ? Les fichiers sont ils interprétés côté serveur (ex: .php, .jsp, etc.) ? Côté client (ex: .html) ?
- [ ] **Upload de fichier ZIP**: dans le cas où les zip sont décompressés. (Voir [ZIP](/ZIP/)).
