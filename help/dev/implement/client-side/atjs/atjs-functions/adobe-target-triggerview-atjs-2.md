---
keywords: adobe.target.triggerView, triggerView, triggerView, Trigger View, at.js, Funktionen, Funktion, viewName, viewname, Ansichtsname, adobe.target.triggerView1
description: Verwenden Sie die Funktion adobe.target.triggerView() für die  [!DNL Adobe Target] .at.js-JavaScript-Bibliothek zur Verwendung in Single Page Applications (SPA). (at.js 2.x)
title: Wie verwende ich die Funktion adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: fe4e607173c760f782035a10f52936d96e9db300
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 21%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird. `adobe.target.triggerView()` sollte für Single Page Applications (SPA) implementiert werden, um den [!UICONTROL Visual Experience Composer] (VEC) zum Erstellen von [!UICONTROL A/B Test]- und [!UICONTROL Experience Targeting] (XT)-Aktivitäten zu verwenden. Wenn `[!UICONTROL adobe.target.triggerView()]` nicht auf der Site implementiert ist, kann VEC nicht für SPA verwendet werden. Weitere Informationen finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Diese Funktion wurde mit at.js 2 eingeführt.*x*. Diese Funktion ist für at.js-Version 1 nicht verfügbar.*x*.

| Parameter | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| viewName | Zeichenfolge | Ja | Geben Sie eine beliebige Zeichenfolge als Namen für Ihre Ansicht an. Dieser Ansichtsname wird im [!UICONTROL Modifications] des VEC angezeigt, damit Marketing-Experten Aktionen erstellen und ihre [!UICONTROL A/B Test]- und [!UICONTROL Experience Targeting]-Aktivitäten ausführen können. |
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

## Beispiel: Beste Kompatibilität für `triggerView()` mit dem [!UICONTROL Adobe Visual Editing Helper extension]

Beachten Sie bei Verwendung der Erweiterung [Adobe Visual Editing Helper“ Folgendes](https://experienceleague.adobe.com/de/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Aufgrund der neuen V3-Manifestrichtlinien von [!DNL Googl]e für [!DNL Chrome]-Erweiterungen muss der [!UICONTROL Visual Editing Helper extension] auf das `DOMContentLoaded`-Ereignis warten, bevor die [!DNL Target] in VEC geladen werden. Diese Verzögerung kann dazu führen, dass Web-Seiten den `triggerView()`-Aufruf auslösen, bevor die Authoring-Bibliotheken bereit sind, was dazu führen kann, dass die Ansicht beim Laden nicht ausgefüllt wird.

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


