---
title: Vergleich von at.js mit der Experience Platform Web SDK
description: Erfahren Sie, wie die at.js-Funktionen im Vergleich zu  [!DNL Experience Platform Web SDK].
keywords: target;adobe target;activity.id;experience.id;renderDecisions;Entscheidungsumfänge;Snippet vorab ausblenden;VEC;Form-Based Experience Composer;xdm;Zielgruppen;Entscheidungen;Umfang;Schema;Systemdiagramm;Diagramm
feature: AEP Web SDK
source-git-commit: d6b93537692a1efbc2650a015f5a44d4fd1fd422
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 5%

---

# Vergleich der at.js-Bibliothek mit der [!DNL Adobe Experience Platform Web SDK]

## Überblick

Dieser Artikel bietet einen Überblick über die Unterschiede zwischen der `at.js`-Bibliothek und der Experience Platform Web SDK.

## Installieren der Bibliotheken

### Installieren von at.js

[!DNL Adobe] können Kundinnen und Kunden die Bibliothek direkt über die Registerkarte [!DNL Adobe Experience Cloud] [!UICONTROL Implementation] herunterladen. Die at.js-Bibliothek wird mit Einstellungen angepasst, die der Kunde hat: clientCode, imsOrgId usw.

### Installieren von Web SDK

Die vordefinierte Version ist in einem CDN verfügbar. Sie können direkt auf Ihrer Seite auf die Bibliothek im CDN verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und nicht minimierten Formaten verfügbar. Die nicht minimierte Version ist zum Debuggen hilfreich.

Weitere [ finden Sie unter „Installieren von Web SDK mithilfe ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/library) JavaScript-Bibliothek“.

## Konfigurieren der Bibliotheken

### Konfigurieren von at.js

Am Ende jeder at.js-Datei sehen Sie einen Abschnitt, in dem [!DNL Adobe] ein Einstellungsobjekt instanziiert und übergibt. Es ist anpassbar, beim Herunterladen füllt Adobe diesen Abschnitt mit aktuellen Kundeneinstellungen.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Weitere Informationen](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)

### Konfigurieren von Platform Web SDK

Die Konfiguration für die SDK erfolgt mit dem Befehl [`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview) . Der `configure` Befehl wird *immer* zuerst aufgerufen.

## Anfordern und automatisches Rendern des Seitenladevorgangs [!DNL Target] Angebote

### Verwenden von at.js

Wenn Sie at.js 2.x verwenden und die Einstellung `pageLoadEnabled,` Bibliotheks-Trigger aktivieren, wird [!DNL Target] Edge mit `execute -> pageLoad` aufgerufen. Wenn alle Einstellungen auf die Standardwerte eingestellt sind, ist keine benutzerdefinierte Codierung erforderlich. Nachdem at.js zur Seite hinzugefügt und vom Browser geladen wurde, wird ein [!DNL Target] Edge-Aufruf ausgeführt.

### Verwenden von [!DNL PLatform Web SDK]

Inhalte, die in [!DNL Target] [Visual Experience Composer](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/visual-experience-composer) erstellt wurden, können von SDK automatisch abgerufen und gerendert werden.

Um [!DNL Target] Angebote anzufordern und automatisch zu rendern, verwenden Sie den Befehl `sendEvent` und setzen die Option `renderDecisions` auf `true.` Dadurch wird die SDK gezwungen, automatisch alle personalisierten Inhalte zu rendern, die für das automatische Rendering geeignet sind.

Beispiel:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

[!DNL Experience Platform Web SDK] sendet automatisch eine Benachrichtigung mit den Angeboten, die von der [!DNL Platform WEB SDK] ausgeführt wurden. Dies ist ein Beispiel dafür, wie die Payload einer Benachrichtigungsanfrage aussieht:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Weitere Informationen](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Anfordern und (*)* automatischen Rendern von Seitenladezielgruppenangeboten

### Verwenden von at.js

Es gibt zwei Möglichkeiten, einen Aufruf an [!DNL Target] Edge auszulösen, der Angebote zum Laden der Seite abruft.

Beispiel 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Beispiel 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions)

### Verwenden von [!DNL Platform Web SDK]

Führen Sie einen `sendEvent` Befehl mit einem speziellen Bereich unter `decisionScopes` aus: `__view__`. [!DNL Adobe] verwendet diesen Umfang als Signal, um alle Seitenladeaktivitäten aus [!DNL Target] abzurufen und alle Ansichten vorab abzurufen. Der [!DNL Platform Web SDK] versucht auch, alle ansichtsbasierten Aktivitäten des VEC auszuwerten. Das Deaktivieren des Vorabrufs von Ansichten wird derzeit in der [!DNL Platform Web SDK] nicht unterstützt.

Für den Zugriff auf Personalisierungsinhalte können Sie eine Rückruffunktion bereitstellen, die aufgerufen wird, nachdem die SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Callback wird als Ergebnisobjekt bereitgestellt, das die Eigenschaft „Vorschläge“ enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält.

Beispiel:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Weitere Informationen](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Anfordern bestimmter formularbasierter Target-Mboxes

### Verwenden von at.js

Mithilfe der `getOffer`-Funktion können Sie F-Aktivitäten abrufen:

Beispiel 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Beispiel 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions.html)

### Verwenden von [!DNL Platform Web SDK]

Sie können [!UICONTROL Form-Based Composer] Aktivitäten abrufen, indem Sie den Befehl `sendEvent` verwenden und die Mbox-Namen unter der Option `decisionScopes` übergeben. Der Befehl `sendEvent` gibt eine Zusage zurück, die mit einem Objekt aufgelöst wird, das die angeforderten Aktivitäten/Vorschläge enthält:

Dieses Code-Fragment zeigt, wie das `propositions`-Array aussieht:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Beispiel:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Weitere Informationen](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Anwenden der [!DNL Target] Aktivitäten

### Verwenden von at.js

Sie können die [!DNL Target] Aktivitäten mithilfe der `applyOffers` anwenden: `adobe.target.applyOffer(options).`

Beispiel:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Weitere Informationen über den `applyOffers`-Befehl finden Sie in der [dedizierten Dokumentation](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2).

### Verwenden von [!DNL Platform Web SDK]

Sie können die [!DNL Target] Aktivitäten mithilfe des Befehls `applyPropositions` anwenden.

Beispiel:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Weitere Informationen über den `applyPropositions`-Befehl finden Sie in der [dedizierten Dokumentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content).

## Tracking von Ereignissen

### Verwenden von at.js

Sie können Ereignisse mithilfe der `trackEvent` oder mithilfe von `sendNotifications.` verfolgen

Diese Funktion löst eine Anforderung zum Melden von Benutzeraktionen aus (wie beispielsweise Klicks und Konversionen). Diese Funktion liefert keine Aktivitäten in der Antwort.

**Beispiel 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Beispiel 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### Verwenden von [!DNL Platform Web SDK]

Sie können Ereignisse und Benutzeraktionen verfolgen, indem Sie den `sendEvent`-Befehl aufrufen, die `_experience.decisioning.propositions` XDM-`fieldgroup` ausfüllen und die `eventType` auf einen von zwei Werten setzen:

* `decisioning.propositionDisplay`: Signalisiert das Rendering der [!DNL Target].
* `decisioning.propositionInteract`: Signalisiert eine Benutzerinteraktion mit der Aktivität wie ein Mausklick.

Die `_experience.decisioning.propositions` XDM-`fieldgroup` ist ein Array von -Objekten. Die Eigenschaften der einzelnen -Objekte werden von dem `result.propositions` abgeleitet, der im `sendEvent`-Befehl zurückgegeben wird: `{ id, scope, scopeDetails }.`

**Beispiel 1: Verfolgen eines `decisioning.propositionDisplay` Ereignisses nach dem Rendern einer Aktivität**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [{
              "id": id,
              "scope": scope,
              "scopeDetails": scopeDetails
            }],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```

**Beispiel 2: Verfolgen eines `decisioning.propositionInteract` Ereignisses nach einem Klick auf eine Metrik**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Weitere Informationen](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content#manual)

**Beispiel 3: Verfolgen eines Ereignisses, das nach einer Aktion ausgelöst wurde**

In diesem Beispiel wird ein Ereignis nachverfolgt, das nach Durchführung einer bestimmten Aktion, z. B. Klicken auf eine Schaltfläche, ausgelöst wurde.
Sie können über das `__adobe.target` Datenobjekt beliebige weitere benutzerdefinierte Parameter hinzufügen.

Sie können auch das `commerce` XDM-Objekt hinzufügen.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## Trigger einer Ansichtsänderung in einem Einzelseiten-Programm

### Verwenden von at.js

Verwenden Sie die `adobe.target.triggerView`. Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird. Die `adobe.target.triggerView()` sollte für Single Page Applications (SPAs) implementiert werden, um den [!UICONTROL Visual Experience Composer] (VEC) zum Erstellen von [!UICONTROL A/B Test]- und [!UICONTROL Experience Targeting] (XT)-Aktivitäten zu verwenden. Wenn `adobe.target.triggerView()` nicht auf der Site implementiert ist, kann VEC nicht für SPAs verwendet werden.

**Beispiel**

```javascript
adobe.target.triggerView("homeView")
```

[Weitere Informationen](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)

### Verwenden von [!DNL Platform Web SDK]

Um einen Trigger oder ein Signal für eine Einzelseiten-[!UICONTROL View Change] auszugeben, legen Sie die Eigenschaft `web.webPageDetails.viewName` unter der Option `xdm` des Befehls `sendEvent` fest. Der [!DNL Platform Web SDK] prüft den Ansichts-Cache, ob Angebote für die in angegebenen `viewName` vorhanden sind, `sendEvent` er sie ausführt und ein Anzeigebenachrichtigungsereignis sendet.

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Weitere Informationen](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)

## So nutzen Sie [!UICONTROL Response Tokens]

Personalization-Inhalte, die von [!DNL Target] zurückgegeben werden, enthalten [Antwort-Token](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens). Antwort-Token sind Details zu Aktivität, Angebot, Erlebnis, Benutzerprofil, geografischen Informationen und mehr. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der [!DNL Target]-Benutzeroberfläche konfiguriert werden.

### Verwenden von at.js

Verwenden Sie benutzerdefinierte at.js-Ereignisse, um auf die [!DNL Target]-Antwort zu warten und die Antwort-Token zu lesen.

**Beispiel**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

### Verwenden von [!DNL Platform Web SDK]

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie [!DNL Experience Platform Web SDK] Version 2.6.0 oder höher verwenden.

Die Antwort-Token werden als Teil der `propositions` zurückgegeben, die im Ergebnis des `sendEvent`-Befehls verfügbar gemacht werden. Jeder Vorschlag enthält ein Array von `items,`, und jedes Element verfügt über ein `meta` Objekt, das mit Antwort-Token gefüllt wird, sofern diese in der [!DNL Target] Admin-Benutzeroberfläche aktiviert sind. [Weitere Informationen](https://experienceleague.adobe.com/en/docs/target/using/administer/response-tokens)

**Beispiel**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Weitere Informationen](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)

## Verwalten von Flackern

### Verwenden von at.js

Mit at.js können Sie ein Flackern verhindern, indem Sie `bodyHidingEnabled: true` so festlegen, dass at.js diejenige ist, um die Sie sich kümmern würden
Vorab-Ausblenden der personalisierten Container, bevor die DOM-Änderungen abgerufen und angewendet werden.

Die Seitenabschnitte, die personalisierte Inhalte enthalten, können vorab ausgeblendet werden, indem die at.js-`bodyHiddenStyle.` überschrieben wird

Standardmäßig blendet `bodyHiddenStyle` die gesamte HTML-`body.` aus

Beide Einstellungen können mit überschrieben werden, `window.targetGlobalSettings.` `window.targetGlobalSettings` vor dem Laden von at.js platziert werden sollten.

### Verwenden von [!DNL Platform Web SDK]

Mit [!DNL Platform Web SDK] kann der Kunde seinen Stil zum Vorab-Ausblenden im configure-Befehl festlegen, wie im folgenden Beispiel gezeigt:

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Beim Laden des asynchronen [!DNL Platform Web SDK] empfiehlt [!DNL Adobe], den folgenden Code-Ausschnitt in die Seite einzufügen, bevor [!DNL Platform Web SDK] eingefügt wird:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Handhabung von A4T

### Verwenden von at.js

Es gibt zwei Arten von A4T-Protokollierung, die mit at.js unterstützt werden:

* Client-seitige Protokollierung in Analytics
* Server-seitige Analytics-Protokollierung

#### Client-seitige Protokollierung in Analytics

**Beispiel 1: Verwenden [!DNL Target] globalen Einstellung**

Die Client-seitige Protokollierung in Analytics kann aktiviert werden, indem `analyticsLogging: client_side` in den at.js-Einstellungen festgelegt oder das `window.targetglobalSettings`-Objekt überschrieben wird.

Wenn diese Option eingerichtet ist, sieht das Format der zurückgegebenen Payload wie folgt aus:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

Die Payload kann dann über den an [!DNL Analytics] weitergeleitet [!DNL  Data Insertion API].

Beispiel 2: Konfiguration in jeder `getOffers`:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Mit diesem Code-Snippet wird die Antwort-Payload wie folgt dargestellt:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Die [!DNL Analytics]-Payload (`tnta`-Token) sollte mit der Dateneinfüge-[!DNL Analytics] in den [-Treffer ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### [!DNL Analytics] Server-seitige Protokollierung

[!DNL Analytics] Server-seitige Protokollierung kann aktiviert werden, indem `analyticsLogging: server_side` in den at.js-Einstellungen festgelegt oder das `window.targetglobalSettings`-Objekt überschrieben wird.

Die Daten fließen dann wie folgt:

![Diagramm mit dem Server-seitigen Analytics-Protokollierungs-Workflow](/help/dev/implement/client-side/aep-web-sdk/assets/a4t-server-side-atjs.png)

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### Verwenden von [!DNL Platform Web SDK]

Web-SDK unterstützt auch:

* Client-seitige Protokollierung in Analytics
* Server-seitige Analytics-Protokollierung

#### [!DNL Analytics] Client-seitige Protokollierung

[!DNL Analytics] Client-seitige Protokollierung ist aktiviert, wenn [!DNL Adobe Analytics] für diese DataStream-Konfiguration deaktiviert ist.

![Diagramm mit dem Client-seitigen Analytics-Protokollierungs-Workflow](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-disabled-datastream-config.png)

Die Kundin bzw. der Kunde hat Zugriff auf das [!DNL Analytics]-Token (`tnta`), das über die [!DNL Analytics]Dateneinfüge-API[ mit ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) geteilt werden muss, indem der `sendEvent`-Befehl verkettet wird und das resultierende Vorschläge-Array iteriert wird.

**Beispiel**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Im Folgenden finden Sie ein Diagramm, das zeigt, wie Daten fließen, wenn [!DNL Analytics] Client-Seite aktiviert ist:

![Datenflussdiagramm in Client-seitiger Analytics-Protokollierung](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-client-side-logging.png)

#### [!DNL Analytics] Server-seitige Protokollierung

[!DNL Analytics] Server-seitige Protokollierung ist aktiviert, wenn [!DNL Analytics] für diese DataStream-Konfiguration aktiviert ist.

![Datenströme -Benutzeroberfläche mit den Analytics-Einstellungen.](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-enabled-datastream-config.png)

Wenn die Server-seitige [!DNL Analytics]-Protokollierung aktiviert ist, wird die A4T-Payload, die für [!DNL Analytics] freigegeben werden muss, damit die [!DNL Analytics]-Berichte die richtigen Impressionen und Konversionen anzeigen, auf Edge Network-Ebene freigegeben, sodass der Kunde keine zusätzliche Verarbeitung durchführen muss.

So fließen Daten in die Systeme, wenn die Server-seitige Analytics-Protokollierung aktiviert ist:

![Diagramm mit dem Datenfluss in der Server-seitigen Analytics-Protokollierung](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-server-side-logging.png)

## Festlegen [!DNL Target] globalen Einstellungen

### Verwenden von at.js

Sie können Einstellungen in der at.js-Bibliothek mithilfe von `window.targetGlobalSettings,` überschreiben, anstatt die Einstellungen in der [!DNL Target]-Benutzeroberfläche oder durch Verwendung von REST-APIs zu konfigurieren.

Die Überschreibung sollte definiert werden, bevor at.js geladen wird, oder alternativ unter Administration > Implementierung > at.js-Einstellungen bearbeiten > Code-Einstellungen > Bibliothekskopfzeile.

Beispiel:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### Verwenden von [!DNL Platform Web SDK]

Diese Funktion wird in Web SDK nicht unterstützt.

## Aktualisieren [!DNL Target] Profilattribute

### Verwenden von at.js

**Beispiel 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Verwenden von [!DNL Platform Web SDK]

Um ein [!DNL Target] zu aktualisieren, verwenden Sie den Befehl `sendEvent` und legen Sie die Eigenschaft `data.__adobe.target` fest, wobei die Schlüsselnamen mit dem Präfix `profile.`

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Wie verwende ich [!DNL Target Recommendations]

### Verwenden von at.js

**Beispiel 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)

### Verwenden von [!DNL Platform Web SDK]

Um [!DNL Recommendations] zu senden, verwenden Sie den Befehl `sendEvent` und legen Sie die `data.__adobe.target` Eigenschaft fest, wobei die Schlüsselnamen mit dem Präfix `entity.`

**Beispiel**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## Wie verwende ich Drittanbieter-IDs?

### Verwenden von at.js

Bei der Verwendung von at.js gibt es mehrere Möglichkeiten, `mbox3rdPartyId` mithilfe von `getOffer,` oder `getOffers` zu senden:

**Beispiel 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Beispiel 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

Oder es gibt eine Möglichkeit, die `mbox3rdPartyId` entweder in `targetPageParams` oder `targetPageParamsAll.` einzurichten

Wenn Sie `targetPageParams` festlegen, sendet es die Anfragen für `target-global-mbox`, die auch als `pag-lLoad` bezeichnet werden.

Die Empfehlung muss mit `targetPageParamsAll` festgelegt werden, da sie bei jeder [!DNL Target] gesendet wird. Der Vorteil der Verwendung von `targetPageParamsAll` besteht darin, dass Sie die `mbox3rdPartyId` auf der Seite einmal definieren können, um sicherzustellen, dass alle [!DNL Target]-Anfragen die richtigen `mbox3rdPartyId.` haben

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### Verwenden von [!DNL Platform Web SDK]

[!DNL Platform Web SDK] unterstützt [!DNL Target] Drittanbieter-ID. Es sind jedoch einige weitere Schritte erforderlich.

Mit Identity Map können Kundinnen und Kunden mehrere Identitäten senden. Alle Identitäten haben einen Namespace. Jeder Namespace kann eine oder mehrere Identitäten aufweisen. Eine bestimmte Identität kann als primär markiert werden. Mit diesem Wissen im Hinterkopf können Sie sehen, welche Schritte zum Einrichten von erforderlich sind, damit [!DNL Platform Web SDK] die [!DNL Target]-Drittanbieter-ID verwenden kann.

1. Richten Sie den Namespace ein, der die [!DNL Target] Drittanbieter-ID auf der Seite Datenstromkonfiguration enthält:

![Datenströme -Benutzeroberfläche mit dem Namespace-Feld für die Target-Drittanbieter-ID](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

1. Senden Sie diesen Identity-Namespace in jedem `sendEvent` wie folgt:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Wie werden Eigenschafts-Token festgelegt

### Verwenden von at.js

Bei der Verwendung von at.js gibt es zwei Möglichkeiten, die Eigenschafts-Token einzurichten: Entweder mit `targetPageParams` oder `targetPageParamsAll.` Mit `targetPageParams` wird das Eigenschafts-Token zum `target-global-mbox`-Aufruf hinzugefügt, aber mit `targetPageParamsAll` wird das Token zu allen [!DNL Target]-Aufrufen hinzugefügt:

**Beispiel 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Beispiel 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Verwenden von [!DNL Platform Web SDK]

Mithilfe von [!DNL Platform Web SDK] können Kundinnen und Kunden die Eigenschaft beim Einrichten der Datenstromkonfiguration unter dem [!DNL Adobe Target]-Namespace auf einer höheren Ebene einrichten:

![Datastreams-Benutzeroberfläche mit den Adobe Target-Einstellungen.](/help/dev/implement/client-side/aep-web-sdk/assets/at-property-setup.png)

Das bedeutet, dass jeder [!DNL Target]-Aufruf für diese spezifische Datenstromkonfiguration dieses Eigenschafts-Token enthält.

## Wie kann ich Mboxes vorab abrufen?

### Verwenden von at.js

Diese Funktion ist nur in at.js 2.x verfügbar. at.js 2.x verfügt über eine neue Funktion namens `getOffers`. Mit der Funktion `getOffers` können Kunden Inhalte für eine oder mehrere Mboxes vorab abrufen. Siehe folgendes Beispiel:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!NOTE]
>
>Adobe empfiehlt sicherzustellen, dass jede `mbox` im `mboxes`-Array über einen eigenen Index verfügt. Normalerweise hat die erste Mbox die nächste `index=0` und so weiter `index=1,`.

### Verwenden von [!DNL Platform Web SDK]

Diese Funktion wird derzeit in [!DNL Platform Web SDK] nicht unterstützt.

## Wie kann ich meine [!DNL Target] debuggen?

### Verwenden von at.js

Die at.js-Bibliothek stellt die folgenden Debugging-Funktionen bereit:

* Mbox deaktivieren - Deaktiviert das Abrufen und Rendern von [!DNL Target], um zu überprüfen, ob die Seite ohne [!DNL Target] Interaktionen beschädigt ist
* Mbox Debug - at.js protokolliert jede Aktion
* Target Trace - mit einem in einem Trace-Objekt generierten Mbox-Trace-Token mit Details, die am Entscheidungsprozess beteiligt waren, ist unter `window.___target_trace` Objekt verfügbar.

>[!NOTE]
>
>Alle diese Debugging-Funktionen sind in [Adobe Experience Platform Debugger mit erweiterten Funktionen ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

### Verwenden von [!DNL Platform Web SDK]

Bei Verwendung von [!DNL Platform Web SDK] stehen mehrere Debugging-Funktionen zur Verfügung:

* Verwenden von [Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* [Web SDK Debug aktiviert](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home)
* Verwenden [ Überwachungs-Hooks für Web SDK](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Verwenden Sie [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home)
* Zielspur