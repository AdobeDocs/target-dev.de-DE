---
keywords: adobe.target.triggerView, triggerView, triggerview, Trigger view, at.js, features, function, viewName, viewname, Ansichtsname, adobe.target.triggerView1
description: Verwenden Sie die Funktion adobe.target.triggerView() für die JavaScript-Bibliothek [!DNL Adobe Target] at.js zur Verwendung in Einzelseiten-Apps (SPA). (at.js 2.x)
title: Wie verwende ich die Funktion adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: fe4e607173c760f782035a10f52936d96e9db300
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 21%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird. `adobe.target.triggerView()` sollte für Einzelseitenanwendungen (SPA) implementiert werden, um die [!UICONTROL Visual Experience Composer] (VEC) zur Erstellung von [!UICONTROL A/B Test] - und [!UICONTROL Experience Targeting] (XT) -Aktivitäten zu verwenden. Wenn `[!UICONTROL adobe.target.triggerView()]` nicht auf der Site implementiert ist, kann VEC nicht für SPA verwendet werden. Weitere Informationen finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Diese Funktion wurde mit at.js 2 eingeführt.*x*. Diese Funktion ist nicht für at.js Version 1 verfügbar.*x*.

| Parameter | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| viewName | Zeichenfolge | Ja | Geben Sie eine beliebige Zeichenfolge als Namen für Ihre Ansicht an. Der Name dieser Ansicht wird im Bedienfeld [!UICONTROL Modifications] des VEC angezeigt, damit Marketing-Experten Aktionen erstellen und ihre XT-Aktivitäten [!UICONTROL A/B Test] und [!UICONTROL Experience Targeting] ausführen können. |
| options | Objekt | Nein |  |
| Optionen > Seite | Boolesch | Nein | **TRUE:** Der Standardwert der Seite ist „wahr“. Bei page=true werden Benachrichtigungen zum Erhöhen der Impressions-Anzahl an das [!DNL Target]-Backend gesendet.<P>Eine Benachrichtigung wird immer standardmäßig gesendet, wenn ein `[!UICONTROL triggerView]` aufgerufen wird, außer wenn &quot;options&quot;> &quot;page&quot;auf &quot;false&quot;gesetzt ist.<P>**FALSE:** Bei page=false werden keine Benachrichtigungen zur Erhöhung der Impressions-Anzahl gesendet. Dieser Ansatz sollte verwendet werden, wenn Sie nur eine Komponente auf einer Seite mit einem Angebot erneut rendern möchten.<P>**Hinweis**: Angebote mit benutzerspezifischem Code im VEC werden nicht erneut gerendert, wenn `[!UICONTROL triggerView()]` mit `{page: false}` als Option aufgerufen wird. |

## Beispiel: True

`[!UICONTROL triggerView()]` -Aufruf zum Senden einer Benachrichtigung an das [!DNL Target] -Backend zur Erhöhung der Aktivitätsimpressionen und anderer Metriken.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Beispiel: False

`[!UICONTROL triggerView()]` -Aufruf, um keine Benachrichtigungen zur Impressions-Zählung an das [!DNL Target] -Backend zu senden.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Beispiel: Versprechen, Verketten mit `getoffers()` und `applyOffers()`

Um `triggerView()` auszuführen, wenn das `getOffers()`-Versprechen aufgelöst wird, ist es wichtig, `triggerView()` auf dem letzten Block auszuführen, wie im folgenden Beispiel gezeigt. Dies ist erforderlich, damit VEC `Views` im Authoring-Modus erkennen kann.

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

Beachten Sie Folgendes bei Verwendung der Erweiterung [Adobe Visual Editing Helper Extension](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Aufgrund der neuen V3-Manifestrichtlinien von [!DNL Googl] e für [!DNL Chrome] -Erweiterungen muss [!UICONTROL Visual Editing Helper extension] auf das `DOMContentLoaded` -Ereignis warten, bevor die [!DNL Target] -Bibliotheken in VEC geladen werden. Diese Verzögerung kann dazu führen, dass Webseiten den Aufruf `triggerView()` auslösen, bevor die Authoring-Bibliotheken bereit sind, was dazu führt, dass die Ansicht beim Laden nicht gefüllt wird.

Um dieses Problem zu beheben, verwenden Sie einen Listener für das page `load` -Ereignis.

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


