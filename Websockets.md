---
title: Websockets
permalink: /Websockets/
---

# Websockets

## Ouverture 

L'ouverture d'une websocket en Javascript est triviale:

``` javascript
var wsUri = "wss://targethost/wsendpoint";
var websocketExample = new WebSocket(wsUri);
websocketExample.close();
```

## Vulnérabilités

Les Websockets ne sont pas soumises à la [Same-Origin Policy](/SOP/) ! Ceci doit être pris en compte lors de leur utilisation. Un risque est présent quand l'établissement de la Websocket repose uniquement sur des cookies utilisateurs.

## Références
- [The problems and some security implications of websockets - Cross-site WebSockets Scripting (XSWS)](https://gist.github.com/subudeepak/9897212)
- [Cross-Site WebSocket Hijacking (CSWSH)](http://www.christian-schneider.net/CrossSiteWebSocketHijacking.html)
