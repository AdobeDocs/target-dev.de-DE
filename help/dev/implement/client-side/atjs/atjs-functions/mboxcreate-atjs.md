---
keywords: mboxCreate, mboxCreate, mbox create, at.js, Funktionen, funktion
description: Verwenden Sie die [!UICONTROL mboxCreate()] -Funktion für [!DNL Adobe Target] JavaScript-Bibliothek at.js , um Angebote auf das nächstgelegene DIV mit dem Klassennamen mboxDefault anzuwenden. (at.js 1.x)
title: Wie verwende ich die [!UICONTROL mboxCreate()] Funktion?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 55%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Führt eine Anforderung aus und wendet das Angebot auf den nächsten DIV-Bereich mit dem Klassennamen „mboxDefault“ an.

>[!NOTE]
>
>Diese Funktion steht nur für at.js, Version 1.*x*, zur Verfügung. Diese Funktion ist mit der Veröffentlichung von at.js 2.x überholt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird.

Diese Funktion wurde vor allem deswegen in at.js integriert, um den Übergang von mbox.js (jetzt nicht mehr unterstützt) zu at.js zu erleichtern. Eine aktuellere Alternative zu `[!UICONTROL mboxCreate()]` ist `[!UICONTROL adobe.target.applyOffer()]`/ `[!UICONTROL adobe.target.getOffer()]` oder die Angular-Richtlinie.

## Beispiel

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## Hinweise

`mboxCreate()` verwendet nun den „json“- statt des „standard“-Endpunkts und wird asynchron ausgelöst. Konsequenzen:

* [Debuggen](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md) verhält sich ein wenig anders.
* Vermeiden Sie Angebotscode, der synchrone, blockierende Aufrufe voraussetzt.

  Ein Beispiel hierfür wären Angebote mit JavaScript-Variablen, die vom Websitecode oder anderen Mboxes verwendet werden, die später auf der Seite auftauchen.

* Stellen Sie sicher, dass eine `<div class="mboxDefault"></div>`vor dem Aufrufen `[!UICONTROL mboxCreate()]`, da at.js keinen für Sie hinzufügt.

* Von leeren `[!UICONTROL mboxCreate()]`-Funktionen als globale Mbox ganz oben auf der Seite wird abgeraten.

  Die automatisch erstellte globale Mbox in at.js ist eine bessere Option, da sie über die `<head>` und kann Inhalte früher zurückgeben.
