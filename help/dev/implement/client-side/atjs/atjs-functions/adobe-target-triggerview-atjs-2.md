---
keywords: adobe.target.triggerView, triggerView, triggerview, Trigger view, at.js, features, function, viewName, viewname, Ansichtsname, adobe.target.triggerView1
description: Verwenden Sie die Funktion adobe.target.triggerView() für die [!DNL Adobe Target] at.js-JavaScript-Bibliothek zur Verwendung in Einzelseiten-Apps (SPA). (at.js 2.x)
title: Wie verwende ich die Funktion adobe.target.triggerView()?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 29%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird. `adobe.target.triggerView()` sollte für Einzelseitenanwendungen (SPA) implementiert werden, um die [!UICONTROL Visual Experience Composer] (VEC) zu erstellen [!UICONTROL A/B-Test] und [!UICONTROL Erlebnis-Targeting] (XT). Wenn `[!UICONTROL adobe.target.triggerView()]` nicht auf der Site implementiert ist, kann VEC nicht für SPA verwendet werden. Weitere Informationen finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Diese Funktion wurde mit at.js 2 eingeführt.*x*. Diese Funktion ist nicht für at.js Version 1 verfügbar.*x*.

| Parameter | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| viewName | Zeichenfolge | Ja | Geben Sie eine beliebige Zeichenfolge als Namen für Ihre Ansicht an. Der Name dieser Ansicht wird im [!UICONTROL Änderungen] Bedienfeld des VEC für Marketing-Experten, um Aktionen zu erstellen und ihre [!UICONTROL A/B-Test] und [!UICONTROL Erlebnis-Targeting] XT-Aktivitäten. |
| options | Objekt | Nein |  |
| Optionen > Seite | Boolesch | Nein | **TRUE:** Der Standardwert der Seite ist „wahr“. Bei page=true werden Benachrichtigungen zum Erhöhen der Impressions-Anzahl an das [!DNL Target]-Backend gesendet.<P>Eine Benachrichtigung wird immer standardmäßig gesendet, wenn eine `[!UICONTROL triggerView]` aufgerufen wird, außer wenn options > page auf false festgelegt ist.<P>**FALSE:** Bei page=false werden keine Benachrichtigungen zum Erhöhen der Impressions-Anzahl gesendet. Dieser Ansatz sollte verwendet werden, wenn Sie nur eine Komponente auf einer Seite mit einem Angebot erneut rendern möchten.<P>**Hinweis**: Angebote mit benutzerspezifischem Code im VEC werden nicht erneut gerendert, wenn `[!UICONTROL triggerView()]` aufgerufen wird mit `{page: false}` als Option. |

## Beispiel: True

`[!UICONTROL triggerView()]` Aufruf zum Senden einer Benachrichtigung an die [!DNL Target] Backend zur Erhöhung von Aktivitätsimpressionen und anderen Metriken.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Beispiel: False

`[!UICONTROL triggerView()]` Aufruf zum Senden von Benachrichtigungen an die [!DNL Target] Backend für Impressions-Zählung.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Beispiel: Versprechen verketten mit `getoffers()` und `applyOffers()`

Ausführen `triggerView()` wenn die `getOffers()` Versprechen aufgelöst wurde, ist es wichtig, `triggerView()` im letzten Block, wie im folgenden Beispiel gezeigt. Dies ist erforderlich, damit VEC `Views` im Authoring-Modus.

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
