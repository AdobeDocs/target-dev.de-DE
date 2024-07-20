---
keywords: adobe.target.triggerView, triggerView, triggerview, Trigger view, at.js, features, function, viewName, viewname, Ansichtsname, adobe.target.triggerView1
description: Verwenden Sie die Funktion adobe.target.triggerView() für die JavaScript-Bibliothek [!DNL Adobe Target] at.js zur Verwendung in Einzelseiten-Apps (SPA). (at.js 2.x)
title: Wie verwende ich die Funktion adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 26%

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
