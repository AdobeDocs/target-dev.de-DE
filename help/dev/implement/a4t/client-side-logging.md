---
title: Client-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Client-seitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe der Experience Platform Web SDK aktivieren.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: Target;A4T;Protokollierung;Web SDK;Experience Platform;Plattform
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Client-seitige Protokollierung für A4T-Daten im [!DNL Experience Platform Web SDK]

Mit dem [!DNL Adobe Experience Platform Web SDK] können Sie [Daten von Adobe Analytics for Target (A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) Client-seitig in Ihrer Web-Anwendung erfassen.

Client-seitige Protokollierung bedeutet, dass relevante [!DNL Target]-Daten Client-seitig zurückgegeben werden, sodass Sie Daten erfassen und für [!DNL Analytics] freigeben können. Diese Option sollte aktiviert werden, wenn Sie Daten manuell über die „Data Insertion [&quot; an Analytics ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html) möchten.

>[!NOTE]
>
>Eine Methode zur Durchführung dieses Vorgangs mit [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) ist derzeit in Entwicklung und wird in naher Zukunft verfügbar sein.

In diesem Dokument werden die Schritte zum Einrichten der Client-seitigen A4T-Protokollierung für die [!DNL Platform Web SDK] beschrieben und Implementierungsbeispiele für gängige Anwendungsfälle bereitgestellt.

## Voraussetzungen  {#prerequisites}

In diesem Tutorial wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten und Prozessen der Verwendung des [!DNL Platform Web SDK] zu Personalisierungszwecken vertraut sind. Lesen Sie die folgende Dokumentation, wenn Sie eine Einführung benötigen:

* [Konfigurieren der Web-SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview)
* [Ereignisse senden](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [Rendern von Personalisierungsinhalten](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## Einrichten [!DNL Analytics] Client-seitigen Protokollierung {#set-up-client-side-logging}

In den folgenden Unterabschnitten wird beschrieben, wie Sie [!DNL Analytics] Client-seitige Protokollierung für Ihre [!DNL Platform Web SDK]-Implementierung aktivieren.

### Aktivieren [!DNL Analytics] Client-seitigen Protokollierung {#enable-analytics-client-side-logging}

Um [!DNL Analytics] Client-seitige Protokollierung für Ihre Implementierung aktivieren zu können, müssen Sie die [!DNL Adobe Analytics]-Konfiguration in Ihrem [Datenstrom“ ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview).

![Analytics-Datenstromkonfiguration deaktiviert](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### Abrufen [!DNL A4T] Daten aus der SDK und Senden an [!DNL Analytics] {#a4t-to-analytics}

Damit diese Berichtsmethode ordnungsgemäß funktioniert, müssen Sie die [!DNL A4T] Daten senden, die mit dem [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)-Befehl im [!DNL Analytics]-Treffer abgerufen wurden.

Wenn [!DNL Target] Edge eine Vorschlagsantwort berechnet, prüft es, ob [!DNL Analytics] Client-seitige Protokollierung aktiviert ist (z. B. wenn [!DNL Analytics] in Ihrem Datenstrom deaktiviert ist). Wenn die Client-seitige Protokollierung aktiviert ist, fügt das System jedem Vorschlag in der Antwort ein [!DNL Analytics]-Token hinzu.

Der Fluss sieht in etwa wie folgt aus:

![Client-seitiger Protokollierungsfluss](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

Im Folgenden finden Sie ein Beispiel für eine `interact`-Antwort, wenn [!DNL Analytics] Client-seitige Protokollierung aktiviert ist. Wenn sich der Vorschlag auf eine Aktivität mit [!DNL Analytics] Berichtsfunktion bezieht, weist er eine `scopeDetails.characteristics.analyticsToken` Eigenschaft auf.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Vorschläge für [!UICONTROL Form-based Experience Composer] Aktivitäten können unter demselben Vorschlag sowohl Inhalts- als auch Klick-Metrik-Elemente enthalten. Anstatt also ein einzelnes Analytics-Token für die Inhaltsanzeige in `scopeDetails.characteristics.analyticsToken` Eigenschaft zu haben, können diese entsprechend sowohl ein Anzeige- als auch ein Klick-Analytics-Token in den `scopeDetails.characteristics.analyticsDisplayToken`- und `scopeDetails.characteristics.analyticsClickToken`-Eigenschaften angegeben haben.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Alle Werte aus `scopeDetails.characteristics.analyticsToken` sowie `scopeDetails.characteristics.analyticsDisplayToken` (für angezeigte Inhalte) und `scopeDetails.characteristics.analyticsClickToken` (für Klickmetriken) sind die A4T-Payloads, die erfasst und als `tnta`-Tag in den Aufruf [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) aufgenommen werden müssen.

>[!IMPORTANT]
>
>Die `analyticsToken`-, `analyticsDisplayToken`- `analyticsClickToken` -Eigenschaften können mehrere Token enthalten, die als einzelne, durch Kommas getrennte Zeichenfolge verkettet sind.
>
>In den im nächsten Abschnitt bereitgestellten Implementierungsbeispielen werden mehrere [!DNL Analytics]-Token iterativ erfasst. Verwenden Sie zum Verketten eines Arrays von [!DNL Analytics]-Token eine Funktion ähnlich der folgenden:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Implementierungsbeispiele {#implementation-examples}

Die folgenden Unterabschnitte zeigen, wie Sie [!DNL Analytics] Client-seitige Protokollierung für gängige Anwendungsfälle implementieren.

### [!UICONTROL Form-Based Experience Composer] Aktivitäten {#form-based-composer}

Sie können die [!DNL Platform Web SDK] verwenden, um die Ausführung von Vorschlägen aus [Adobe Target Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)-Aktivitäten zu steuern.

Wenn Sie Vorschläge für einen bestimmten Entscheidungsumfang anfordern, enthält der zurückgegebene Vorschlag das entsprechende [!DNL Analytics]-Token. Best Practice ist es, den [!DNL Experience Platform Web SDK] `sendEvent`-Befehl zu verketten und durch die zurückgegebenen Vorschläge zu iterieren, um sie auszuführen, während gleichzeitig die [!DNL Analytics]-Token erfasst werden.

Sie können einen `sendEvent`-Befehl für einen [!UICONTROL Form-Based Experience Composer] Aktivitätsbereich wie den folgenden Trigger ausführen:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Von hier aus müssen Sie Code implementieren, um die Vorschläge auszuführen und eine Payload zu erstellen, die letztendlich an [!DNL Analytics] gesendet wird. Dies ist ein Beispiel dafür, was `results.propositions` enthalten könnte:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Um das [!DNL Analytics]-Token aus einem Vorschlag mit Inhaltselementen zu extrahieren, können Sie eine Funktion ähnlich der folgenden implementieren:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Ein Vorschlag kann verschiedene Arten von Elementen aufweisen, wie in der `schema` Eigenschaft des betreffenden Elements angegeben. Für [!UICONTROL Form-Based Experience Composer] Aktivitäten werden vier Schemata für Vorschlagselemente unterstützt:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` und `JSON_SCHEMA` sind die Schemata, die den Typ des Angebots widerspiegeln, während `MEASUREMENT_SCHEMA` die Metriken widerspiegeln, die an ein DOM-Element angehängt werden sollen.

[!DNL Analytics] Payloads für Klickmetriken sollten erfasst und getrennt von Inhaltselementen an [!DNL Analytics] gesendet werden, und zwar zu dem Zeitpunkt, zu dem der Besucher tatsächlich auf den zuvor angezeigten Inhalt klickt.

Die folgende Hilfsfunktion zum Abrufen der Klickmetrik von A4T-Payloads ist in diesem Fall praktisch:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Zusammenfassung der Implementierung {#implementation-summary}

Zusammenfassend lässt sich sagen, dass beim Anwenden [!UICONTROL Form-Based Experience Composer] Aktivitäten mit dem [!DNL Experience Platform Web SDK] die folgenden Schritte ausgeführt werden müssen:

1. Senden eines Ereignisses, das [!UICONTROL Form-Based Experience Composer] Aktivitätsangebote abruft;
1. Anwenden der Inhaltsänderungen auf die Seite
1. Senden des `decisioning.propositionDisplay` Benachrichtigungsereignisses;
1. Erfassen Sie die [!DNL Analytics] Display-Token aus der SDK-Antwort und erstellen Sie eine Payload für den [!DNL Analytics].
1. Senden der Payload an [!DNL Analytics] mithilfe der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Wenn in den zugestellten Vorschlägen Klickmetriken vorhanden sind, sollten Klick-Listener so eingerichtet werden, dass bei einem Klick das `decisioning.propositionInteract` Benachrichtigungsereignis gesendet wird. Der `onBeforeEventSend`-Handler sollte so konfiguriert sein, dass beim Abfangen `decisioning.propositionInteract` Ereignisse die folgenden Aktionen auftreten:
   1. Erfassen der Klick-[!DNL Analytics]-Token aus `xdm._experience.decisioning.propositions`
   1. Senden des Klick-[!DNL Analytics]-Treffers mit der erfassten [!DNL Analytics]-Payload über die [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### [!UICONTROL Visual Experience Composer] (VEC)-Aktivitäten {#visual-experience-composer-acitivties}

Mit dem [!DNL Platform Web SDK] können Sie Angebote verarbeiten, die mit [Visual Experience Composer (VEC) erstellt wurden](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>Die Schritte zur Implementierung dieses Anwendungsfalls ähneln den Schritten für [Form-Based Experience Composer activities](#form-based-composer). Weitere Informationen finden Sie im vorherigen Abschnitt .

Wenn das automatische Rendering aktiviert ist, können Sie die [!DNL Analytics] Token aus den Vorschlägen erfassen, die auf der Seite ausgeführt wurden. Best Practice ist es, den [!DNL Experience Platform Web SDK] `sendEvent`-Befehl zu verketten und durch die zurückgegebenen Vorschläge zu iterieren, um die Vorschläge zu filtern, die Web SDK gerendert haben soll.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Verwenden von `onBeforeEventSend` zur Verarbeitung von Seitenmetriken {#using-onbeforeeventsend}

Mithilfe [!DNL Adobe Target] Aktivitäten können Sie verschiedene Metriken auf der Seite einrichten, entweder manuell an das DOM angehängt oder automatisch an das DOM angehängt (von VEC erstellte Aktivitäten). Bei beiden Typen handelt es sich um eine verzögerte Endbenutzerinteraktion auf der Web-Seite.

Daher empfiehlt es sich, [!DNL Analytics] Payloads mithilfe des `onBeforeEventSend`-[!DNL Adobe Experience Platform Web SDK]-Hooks zu erfassen. Der `onBeforeEventSend`-Hook sollte mit dem `configure`-Befehl konfiguriert werden und wird für alle Ereignisse übernommen, die über den Datenstrom gesendet werden.

Im Folgenden finden Sie ein Beispiel dafür, wie `onBeforeEventSent` so konfiguriert werden können, dass der Trigger [!DNL Analytics] Treffer gelangt:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde die Client-seitige Protokollierung für A4T-Daten im [!DNL Platform Web SDK] behandelt. Weitere Informationen zum Umgang mit [4T-Daten in Edge Network finden ](/help/dev/implement/a4t/server-side-a4t.md) im Handbuch zur Server-seitigen Protokollierung.