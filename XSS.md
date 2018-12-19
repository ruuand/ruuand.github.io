---
title: Cross Site Scripting
permalink: /XSS/
---

# Cross-Site Scripting

## Payloads

Voir [PayloadAllTheThings](https://github.com/ruuand/PayloadsAllTheThings/tree/master/XSS%20injection)

## Events JS

Liste d'events JS:

``` text
onAbort
onActivate
onAfterPrint
onAfterUpdate
onBeforeActivate
onBeforeCopy
onBeforeCut
onBeforeDeactivate
onBeforeEditFocus
onBeforePaste
onBeforePrint
onBeforeUnload
onBeforeUpdate
onBegin
onBlur
onBounce
onCellChange
onChange
onClick
onContextMenu
onControlSelect
onCopy
onCut
onDataAvailable
onDataSetChanged
onDataSetComplete
onDblClick
onDeactivate
onDrag
onDragEnd
onDragLeave
onDragEnter
onDragOver
onDragDrop
onDragStart
onDrop
onEnd
onError
onErrorUpdate
onFilterChange
onFinish
onFocus
onFocusIn
onFocusOut
onHashChange
onHelp
onInput
onKeyDown
onKeyPress
onKeyUp
onLayoutComplete
onLoad
onLoseCapture
onMediaComplete
onMediaError
onMessage
onMouseDown
onMouseEnter
onMouseLeave
onMouseMove
onMouseOut
onMouseOver
onMouseUp
onMouseWheel
onMove
onMoveEnd
onMoveStart
onOffline
onOnline
onOutOfSync
onPaste
onPause
onPopState
onProgress
onPropertyChange
onReadyStateChange
onRedo
onRepeat
onReset
onResize
onResizeEnd
onResizeStart
onResume
onReverse
onRowsEnter
onRowExit
onRowDelete
onRowInserted
onScroll
onSeek
onSelect
onSelectionChange
onSelectStart
onStart
onStop
onStorage
onSyncRestored
onSubmit
onTimeError
onTrackChange
onUndo
onUnload
onURLFlip
seekSegmentTime
```

## Exploitation

Cette section contient des tips & trics sur l'exploitation de XSS.

### ASP.Net
ASP.Net a le mécanisme de "Request Validation" qui bloque de nombreuses tentatives XSS. Globalement tout payload de la forme "<a" (où a est une lettre ou le caractère ! sera bloqué).

Quelques bypass sont possibles:
- Sur les vieilles versions d'IE le payload <#tag
- Si on a une stored il est possible d'injecter un payload en unicode (voir [Bypassing ASP.NET “ValidateRequest” for Stored XSS attacks](https://infosecauditor.wordpress.com/2013/05/27/bypassing-asp-net-validaterequest-for-script-injection-attacks/)). Ceci est dû à une conversion qui est faite par la base de données (les caractères unicodes étant convertis en leur équivalent "standard"): 
``%uff1cscript%uff1ealert('XSS');%uff1c/script%uff1e``
- Sur les vieilles versions de IE et de ASP.net (patch en 2007) le payload suivant marche: ```</XSS STYLE=xss:expression(alert('XSS'))>```

D'autres bypass [Bypassing .Net ValidateRequest](http://www.procheckup.com/media/39734/bypassing-dot-net-validaterequest.pdf)

### Champs hidden

Il est possbible d'exploiter une XSS dans un champ hidden. Voir [XSS in Hidden Input Fields](http://blog.portswigger.net/2015/11/xss-in-hidden-input-fields.html)

## Références
- [JSFuck](http://www.jsfuck.com/)
- [Master the art of Cross Site Scripting](https://brutelogic.com.br/blog/)
- [XSS without event handlers](https://brutelogic.com.br/blog/xss-without-event-handlers/): pour les situations où les events du type onerror sont bloqués
- [XSS Filter Evasion](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)
- [PassiveXssScan](https://github.com/jkadijk/burp-plugins): un plugin pour identifier automatiquement les éléments "reflected" dans Burp.

### Challenges
- [FindBUG XSS Challenge](http://blog.bi.tk/2017/01/20/findbug/)
