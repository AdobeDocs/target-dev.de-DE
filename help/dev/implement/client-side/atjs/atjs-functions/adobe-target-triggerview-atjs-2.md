---
keywords: adobe.target.triggerView, triggerView, triggerView, Trigger View, at.js, Funktionen, Funktion, viewName, viewname, Ansichtsname, adobe.target.triggerView1
description: Verwenden Sie die Funktion adobe.target.triggerView() für die  [!DNL Adobe Target] .at.js-JavaScript-Bibliothek zur Verwendung in Single Page Applications (SPAs). (at.js 2.x)
title: Wie verwende ich die Funktion adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
TQID: https://experienceleague.adobe.com/pBC1GRKG0mxeaZ1hfaByKv2tu-XScrSJfm7lUw-3yKw
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 19%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird. `adobe.target.triggerView()` sollten für Single Page Applications (SPAs) implementiert werden, um die Aktivitäten [!UICONTROL Visual Experience Composer] (VEC) zum Erstellen von [!UICONTROL A/B-] und [!UICONTROL Experience Targeting] (XT) zu verwenden. Wenn `[!UICONTROL adobe.target.triggerView()]` nicht auf der Site implementiert ist, kann VEC nicht für SPAs verwendet werden. Weitere Informationen finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Diese Funktion wurde mit at.js 2.*x* eingeführt. Diese Funktion ist nicht verfügbar für at.js-Version 1.*x*.

| Parameter | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| viewName | Zeichenfolge | Ja | Geben Sie eine beliebige Zeichenfolge als Namen für Ihre Ansicht an. Dieser Ansichtsname wird im Bedienfeld [!UICONTROL Änderungen] des VEC angezeigt, damit Marketing-Experten Aktionen erstellen und ihre [!UICONTROL A/B-Test] und [!UICONTROL Erlebnis-Targeting] XT-Aktivitäten ausführen können. |
| options | Objekt | Nein |  |
| Optionen > Seite | Boolesch | Nein | **TRUE:** Der Standardwert der Seite ist „wahr“. Bei page=true werden Benachrichtigungen zum Erhöhen der Impressions-Anzahl an das [!DNL Target]-Backend gesendet.<P>Eine Benachrichtigung wird immer standardmäßig gesendet, wenn ein `[!UICONTROL triggerView]` aufgerufen wird, es sei denn, „Optionen“ > „Seite“ ist auf „false“ festgelegt.<P>**FALSE:** Wenn page=false ist, werden keine Benachrichtigungen gesendet, um die Anzahl der Impressionen zu erhöhen. Dieser Ansatz sollte verwendet werden, wenn Sie eine Komponente nur auf einer Seite mit einem Angebot erneut rendern möchten.<P>**Hinweis**: Angebote mit benutzerdefiniertem Code in VEC werden nicht erneut gerendert, wenn `[!UICONTROL triggerView()]` mit `{page: false}` als Option aufgerufen wird. |

## Beispiel: True

`[!UICONTROL triggerView()]` Aufruf zum Senden einer Benachrichtigung an das [!DNL Target]-Backend zum Erhöhen von Aktivitätsimpressionen und anderen Metriken.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Beispiel: False

`[!UICONTROL triggerView()]` Aufruf von , um keine Benachrichtigungen zur Impression-Zählung an das [!DNL Target]-Backend zu senden.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Beispiel: Promise-Verkettung mit `getoffers()` und `applyOffers()`

Um `triggerView()` auszuführen, wenn die `getOffers()` aufgelöst ist, ist es wichtig, `triggerView()` auf dem endgültigen Block auszuführen, wie im folgenden Beispiel gezeigt. Dies ist erforderlich, damit VEC `Views` im Authoring-Modus erkennen kann.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## Beispiel: Optimale Kompatibilität für `triggerView()` mit der Erweiterung [!UICONTROL Adobe Visual Editing Helper]

Beachten Sie bei der Verwendung der [Adobe Visual Editing Helper-Erweiterung Folgendes](https://experienceleague.adobe.com/de/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Aufgrund der neuen V3-Manifestrichtlinien von [!DNL Googl]e für [!DNL Chrome]-Erweiterungen muss die Erweiterung [!UICONTROL Visual Editing Helper] auf das `DOMContentLoaded`-Ereignis warten, bevor die [!DNL Target]-Bibliotheken in VEC geladen werden. Diese Verzögerung kann dazu führen, dass Web-Seiten den `triggerView()`-Aufruf auslösen, bevor die Authoring-Bibliotheken bereit sind, was dazu führen kann, dass die Ansicht beim Laden nicht ausgefüllt wird.

Um dieses Problem zu beheben, verwenden Sie einen Listener für das `load`.

Im Folgenden finden Sie eine Beispielimplementierung:

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```




