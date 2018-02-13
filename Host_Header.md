---
title: Host (Header)
permalink: /Host_Header/
---

# Host (Header)

Le header **Host** est utilisé pour déterminer le Hostname auquel on cherche à accéder. L'application peut répondre de plusieurs manières:
- Ignorer le hostname: dans ce cas on devrait avoir la même application en tapant directement sur l'IP.
- Changer l'application: c'est généralement le cas si on a un reverse proxy ou des virtual hosts.

## Références
- [Cracking the Lens: Targeting HTTP's Hidden Attack-Surface](http://blog.portswigger.net/2017/07/cracking-lens-targeting-https-hidden.html): attaques sur les équipements qui font des actions en fonction du champ Host (Proxy, Cache, etc.).
- [Don't Trust the Host Header for Sending Password Reset Emails](https://lightningsecurity.io/blog/host-header-injection/): le hostname est utilisé pour générer les mails de récupération de mot de passe (lien de la forme http://$HOST/password.php)
