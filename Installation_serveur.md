---
title: Installation serveur
permalink: /Installation_serveur/
---

Installation sur Intel NUC
--------------------------

- Prendre une image .iso de Debian. Choisir le CD-1. - Mettre l'image sur une clé USB avec Unetbootin - Installation. Décocher "Environnement de bureau" quand c'est proposé. - Skipper toutes les options nécessitant une connexion internet - Une fois l'installation faite, il faut installer les drivers pour l'ethernet (LINK) - Installer les paquets de gcc à partir de la clé USB (mettre <file:///>) - Mettre les drivers et le paquet de make sur une clé USB - Installer le paquet de make - Compiler les sources du driver. Si nécessaire modifier le Makefile pour remplacer \*gcc\* par \*gcc-version\* - Modifier /etc/network/interfaces - Configurer un serveur NTP

Serveur mail (Postfix + Dovecot)
--------------------------------

Le guide suivant permet l'installation d'un serveur mail. Celui-ci utilise les différents comptes unix. Il est possible de créer des alias (/etc/aliases). Un lien est présent dans le guide pour l'installation d'utilisateurs virutles. <http://www.digitalocean.com/community/tutorials/how-to-set-up-a-postfix-e-mail-server-with-dovecot> <http://blog.rom1v.com/2009/11/installer-un-webmail-roundcube-sur-ubuntu-server/>

RoundCube
---------

Installation d'un webmail <http://blog.rom1v.com/2009/11/installer-un-webmail-roundcube-sur-ubuntu-server/>

Installation TinyTinyRSS
------------------------

<http://blog.rom1v.com/2009/11/installer-un-webmail-roundcube-sur-ubuntu-server/>

Installation OwnCloud
---------------------

Guide: <http://software.opensuse.org/download.html?project=isv:ownCloud:community&package=owncloud> Ajout dépôt contenant ownCloud echo 'deb <http://download.opensuse.org/repositories/isv:/ownCloud:/community/Debian_7.0/> /' &gt;&gt; /etc/apt/sources.list.d/owncloud.list apt-get update apt-get install owncloud

Ajout de la clé du dépôt wget <http://download.opensuse.org/repositories/isv:ownCloud:community/Debian_7.0/Release.key> apt-key add - &lt; Release.key

Créer un virtual host pointant vers /var/www/owncloud Aller à l'interface web (https://cloud.ruuand.fr) pour l'installation Donner le mot de passe root de mysql. Un utilisateur dédié sera créé.

Migration mbox -&gt; maildir
----------------------------

<http://perfectmaildir.home-dn.net/>

ZNC
---

<https://www.digitalocean.com/community/tutorials/how-to-install-znc-an-irc-bouncer-on-an-ubuntu-vps>

[Catégorie:Méthodologies](/Catégorie:Méthodologies "wikilink")