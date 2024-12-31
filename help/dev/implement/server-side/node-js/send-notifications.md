---
title: Senden von Anzeige- oder Klickbenachrichtigungen an  [!DNL Adobe Target] mithilfe der Node.js-SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klick-Benachrichtigungen an senden können [!DNL Adobe Target]  um Messungen und Berichte durchzuführen.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 4%

---

# Senden von Benachrichtigungen (Node.js)

## Beschreibung

`[!UICONTROL sendNotifications()]` wird verwendet, um Anzeige- oder Klick-Benachrichtigungen zur Messung und Berichterstellung an [!DNL Adobe Target] zu senden.

>[!NOTE]
>
>Wenn sich ein `execute` mit erforderlichen Parametern in der Anfrage selbst befindet, wird die Impression automatisch für qualifizierte Aktivitäten inkrementiert.

SDK-Methoden, die eine Impression automatisch inkrementieren:

* `getOffers()`
* `getAttributes()`

Wenn ein `prefetch` innerhalb der Anfrage übergeben wird, wird die Impression für die Aktivitäten mit Mboxes innerhalb des `prefetch`-Objekts nicht automatisch inkrementiert. `sendNotifications()` müssen für vorab abgerufene Erlebnisse verwendet werden, um Impressionen und Konversionen zu erhöhen.

## Methode

### erstellen

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung |
| --- | --- | --- | --- |
| Anfrage | Objekt | Ja | Keine |

## Beispiel

Erstellen wir zunächst die Target-D/-API-Anfrage zum vorherigen Abrufen von Inhalten für die `home`- und `product1`-Mboxes.

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

Eine erfolgreiche Antwort enthält ein [!UICONTROL Target Delivery API] Antwortobjekt, das vorab abgerufene Inhalte für die angeforderten Mboxes enthält. Ein Beispiel für ein `targetResponse.response` kann wie folgt aussehen:

### Node.js

```js {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Beachten Sie die Mbox-`name` und `state` Felder sowie das `eventToken` Feld in jeder der [!DNL Target] Inhaltsoptionen. Diese sollten in der `sendNotifications()`-Anfrage angegeben werden, sobald jede Inhaltsoption angezeigt wird. Angenommen, die `product1`-Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token entsprechend dem [!DNL Target] Angebot in der Prefetch-Antwort eingeschlossen haben. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie über die `sendNotifications()`-API-Methode an [!DNL Target] senden:

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
