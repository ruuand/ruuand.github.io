---
title: Android
permalink: /Android/
---

# Android

## Décompilation d'APK

Pour décompiler APK on peut utiliser apktool. Cet outil va permettre de récupérer le code .smali, les ressources et également le Manifest

``` bash
apktool d firefox.apk
```

Si on effectue des modifications il est alors possible de le recompiler:

``` bash
apktool b firefox/ -o newfirefox.apk
```

On peut récupérer le code source sous forme de .jar avec dex2jar. On peut ensuite le visualiser avec jd-gui (http://jd.benow.ca/)

``` bash
d2j-dex2jar diva-beta.apk
```

Alternativement on peut utiliser jadx pour générer directement le code .java.

**Note:** il peut arriver que jadx et dex2jar n'arrivent pas à decompiler une fonction / classe.

## Analyse des permissions

Permissions Android définies dans AndroidManifest.xml. Contient également les services, versions de SDK supportées, intents, receivers, etc. Le fichier AndroidManifest.xml n'est pas directement lisible (il est nécessaire de le décoder avec apktool). Regarder les permissions permet notamment d'identifier des applications malveillantes.

Il peut arriver que l'application définisse des permissions qui peuvent être utilisées par d'autres applications. Dans certains cas ces permissions "customs" sont mal protégées et peuvent être exploitées par des applications malveillantes (voir Advanced Drozer Kung Fu - PentesterAcademy)

A revoir: <http://resources.infosecinstitute.com/cracking-damn-insecure-and-vulnerable-app-diva-part-4/#article>

## Signing

Les applications doivent être signées (pas d'autorité de certification). On peut signer une application avec keytool (génération de clé) et jarsigner (pour signer avec la clé générée). Ceci est nécessaire quand on modifie une application.

Pluisuers fichiers sont liés au processus de signature:

-   META-INF/MANIFEST.MSF: déclaration des ressources
-   META-INF/CERT.RSA: Clé Publique
-   META-INF/CERT.SF: Toutes les ressources signées

**Note:** les informations contenues sont faiblement utiles pour un TI classique. Possiblement pus intéressant dans le cas de malwares (réutilisation de la clé).

## Content provider

Composant qui permet d'intéragir avec des bases de données SQLite, fichiers XML, etc.

Les interactions avec les content providers utilisent souvent des chaînes de la forme "<content://>", qu'il est donc possible de chercher dans le code source / code smali.

Il est possible d'interagir avec les content providers et adb shell:

``` bash
adb shell content query --uri content://com.threebanana.notes.provider.NotePad/notes # Permet d'intéragir avec le content providers gérant les notes
```

Il est possible d'exploiter un Content Provider vulnérable pour bénéficier de privilèges additionels (ex: une appli malveillante utilise le Content Provider d'Adobe Reader pour obtenir un accès à la carte SD)

## Analyse dynamique

L'analyse dynamique consiste à executer l'application pour analyser son comportement.

### Android Debug Bride

Android Debug Bridge (adb) est un outil très utile lors des pentests Android.

Les principales commandes sont les suivantes

``` bash
adb connect 192.168.1.44 # connecte adb au device
adb devices # liste les devices connectés
adb shell # ouvre un shell sur le device
adb push test.txt /mnt/sdcard # upload le fichier test.txt sur la carte SD
adb pull /mnt/sdcard/test.txt test.txt # download de la carte SD vers le système de fichier
adb shell ls /mnt/card # execute une commande dans le shell sans l'ouvrir
adb install com.threebanana.notes # installe l'application
adb uninstall com.threebanana.notes # désinstalle
adb backup com.threebanana.notes -f folder # fait un backup des données de l'applications
adb logcat # capture l'ensemble des logs du téléphone
adb shell 'pm list packages -f' # List les packages installés
```

Ensuite il est possible d'executer les commandes linux traditionnelles dans le shell.

### Stockage de données

Avec adb il est possible de regarder les données sauvegardées par l'application. Celles-ci peuvent être stockées à plusieurs endroits:

-   shared_prefs: il s'agit de fichiers xml situés dans /data/data/com.application/shared_prefs/
-   Bases de données sqlite: situées dans /data/data/com.application/databases/. Les commandes utiles sont:
    -   Ouvrir une base de données:
        ``` bash
        sqlite3 database.db
        ```

    -   Afficher les tables de la base de données:
        ``` bash
        .tables
        ```
-   Fichiers dans le répertoire de l'application (/data/data/com.application)
-   Fichiers sur la carte SD. Ceci est critique car n'importe quelle application pourrait ensuite y accéder. (getExternalStorageDirectory)

Plusieurs points à vérifier:

-   Quelles sont les données stockées ?
-   Les données sont elles chiffrées ?
-   Le chiffrement est il réversible ? (Si aucun secret n'est demandé lors de l'utilisation de l'application alors il l'est)

### Logcat

Il est possible de filtrer si on connait le bon process id (avec un ps | grep app)

``` bash
adb shell ps | grep diva # on récupére le PID de l'application DIVA
adb logcat | grep -i 1297 # on affiche le logcat correspondant au PID de DIVA
```

Les éléments intéressants dans les logs sont:

-   Informations pour obtenir une meilleure compréhension de l'application.
-   Informations sensibles (ex: Error the password "pasword" is invalid)
-   Messages d'erreurs lors d'attaques sur l'application she

**A vérifier**: A noter que les informations contenues dans logcat sont accessibles à toutes les applications.

### Input validation

Des possibilités existent aussi:

-   Injections SQL sur les bases de données locales
-   Mauvaise validation d'inputs

### Librairies tierces

Des librairies tierces peuvent être utilisées (dans /data/data/com.application/libs) et son potentiellement vulnérables. Il est possible d'avoir certaines informations sur celles-ci avec:

``` bash
strings lib.so
```

### SSL Pinning

Il existe de nombreuses méthodes pour bypasser SSL Pinning:

-   [Bypassing SSL Pinning on Android via Reverse Engineering](http://www.security-assessment.com/files/documents/whitepapers/Bypassing%20SSL%20Pinning%20on%20Android%20via%20Reverse%20Engineering.pdf)
-   [Android SSL TrustKiller](https://github.com/iSECPartners/Android-SSL-TrustKiller)
-   [Android SSL Bypass](https://github.com/iSECPartners/android-ssl-bypass)

### Drozer

Framework pour faire de l'audit sur des applications Android.

Modules:

-   Lister les content providers pour une application
-   Requêter un content provider (normalement drozer ne devrait pas avoir de permission de requêter les content providers "sensibles")

Le rôle de Drozer semble principalement être la simulation d'une application malveillante, pour voir quelles informations cette application pourrait récupérer sur des applications cibles.

On peut modifier Drozer pour tenter d'exploiter les permissions "custom" définies par des applications.

Il est possible de créer des scripts pour Drozer.

### Hooking & Debugging

Quelques outils:

-   Andbug (https://github.com/swdunlop/AndBug)
-   Java Debugger
-   Introspy
-   Cydia Substrate

#### Andbug

(https://github.com/swdunlop/AndBug)

On peut lancer le shell andbug avec le PID de l'application qu'on souhaite hooker:

``` bash
adb shell ps | grep application
andbug shell --pid 1662
```

Une fois dans le shell on peut faire différentes actions:

``` python
>> classes # liste l'ensemble des classes chargées
>> classes com.android.insecurebank # idem mais fait un grep pour ne garder que ce qui est pertinent
>> methods com.android.insecurebankv2.DoTransfer # liste les méthodes d'une classe
```

<http://resources.infosecinstitute.com/android-hacking-and-security-part-23-introduction-to-debugging-android-apps-using-andbug/>

#### Java Debugger

Il est possible d'utiliser le debugger Java pour se hooker à une application et modifier à la volée le comportement de celle-ci.

Il faut d'abord lier jdb et l'application:

``` bash
adb shell ps | grep com.application # On récupère le PID
adb forward tcp:[localport] jdwp:[pid application]
jdb -attach localhost:[localport]
```

On peut ensuite récupérer des informations de manière similaire à Andbug (mais sans les filtres):

``` bash
classes # pour lister les classes
methods com.android.insecurebank.RestClient # pour lister les méthodes
```

La partie plus intéressante consiste à set des breakpoints:

``` bash
stop in com.android.insecurebank.RestClient.dotransfer
```

Quand on atteint le breakpoint on a différentes possibilités:

``` bash
locals # liste les variables locales et leur valeur
set amount="2000" # modifie une variable à la volée
```

A tester: évaluation d'une fonction à la volée.

MitM
----

On a les éléments suivants:

-   Ordinateur connecté au Wi-Fi et au réseau ethernet. Définir la route 0.0.0.0 comme étant celle sur l'ethernet. Burp redirigera le traffic reçu sur cette route.
-   Android connecté au Wi-Fi: Configurer le proxy Wi-Fi de l'Android pour pointer vers la machine avec Burp.

## Emulation
### Android Studio

```
cd "C:\Users\[user]\AppData\Local\Android\Sdk\emulator"
emulator.exe -writable-system -camera-back none -camera-front none -netdelay none -netspeed full -avd "Pentest_Device_4.4_" -http-proxy 127.0.0.1:8080
```

### Ressources

- [MobileApp-Pentest-Cheatsheet](https://github.com/tanprathan/MobileApp-Pentest-Cheatsheet)
- [Android Security Awesome](https://github.com/ashishb/android-security-awesome)
- [Tests d’intrusion d’applications Android (XMCO)](https://www.xmco.fr/actu-secu/XMCO-ActuSecu-41-Tests-Intrusion-Android.pdf)
