---
keywords: mboxCreate, mboxCreate, mbox create, at.js, Funktionen, Funktion
description: Verwenden Sie die [!UICONTROL mboxCreate()] für die JavaScript [!DNL Adobe Target] Bibliothek „at.js“, um Angebote auf das nächstgelegene DIV mit dem mboxDefault-Klassennamen anzuwenden. (at.js 1.x)
title: Wie verwende ich die [!UICONTROL mboxCreate()]?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
TQID: https://experienceleague.adobe.com/hCEKL9RPtqIbMVEouzObjU6dc7TKl1hBtKZ1jEdicRE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 211
ht-degree: 41%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Führt eine Anforderung aus und wendet das Angebot auf den nächsten DIV-Bereich mit dem Klassennamen „mboxDefault“ an.

>[!NOTE]
>
>Diese Funktion ist nur für at.js-Versionen 1.*x* verfügbar. Diese Funktion wird seit der Veröffentlichung von at.js 2.x nicht mehr unterstützt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird.

Diese Funktion ist in at.js integriert, um vor allem den Übergang von mbox.js (inzwischen nicht mehr unterstützt) zu at.js zu erleichtern. Eine aktuellere Alternative zu `[!UICONTROL mboxCreate()]` ist `[!UICONTROL adobe.target.applyOffer()]`/ `[!UICONTROL adobe.target.getOffer()]` oder die Angular-Richtlinie.

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

* Verwenden Sie vor dem Aufrufen von `[!UICONTROL mboxCreate()]` unbedingt `<div class="mboxDefault"></div>`, da at.js keine für Sie hinzufügen wird.

* Von leeren `[!UICONTROL mboxCreate()]`-Funktionen als globale Mbox ganz oben auf der Seite wird abgeraten.

  Die automatisch erstellte globale Mbox in at.js ist eine bessere Option, da sie von der `<head>` ausgelöst wird und Inhalte früher zurückgeben kann.
