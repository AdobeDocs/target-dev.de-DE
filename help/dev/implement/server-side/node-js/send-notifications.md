---
title: Anzeigen- oder Klickbenachrichtigungen senden an [!DNL Adobe Target] Verwenden des Node.js-SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klickbenachrichtigungen an senden können. [!DNL Adobe Target] für die Messung und Berichterstellung.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

# Benachrichtigungen senden (Node.js)

## Beschreibung

`[!UICONTROL sendNotifications()]` wird verwendet, um Anzeigen- oder Klickbenachrichtigungen an zu senden [!DNL Adobe Target] für die Messung und Berichterstellung.

>[!NOTE]
>
>Wenn ein `execute` -Objekt mit erforderlichen Parametern in der Anfrage selbst enthalten ist, wird die Impression für qualifizierte Aktivitäten automatisch inkrementiert.

SDK-Methoden, die eine Impression automatisch erhöhen, sind:

* `getOffers()`
* `getAttributes()`

Wenn eine `prefetch` -Objekt innerhalb der Anfrage übergeben wird, wird die Impression nicht automatisch für die Aktivitäten mit Mboxes innerhalb der `prefetch` -Objekt. `sendNotifications()` muss für vorab abgerufene Erlebnisse zur Erhöhung von Impressionen und Konversionen verwendet werden.

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

Erstellen wir zunächst die Target DBereitstellungs-API-Anfrage zum Vorabruf von Inhalten für die `home` und `product1` Mboxes verwenden.

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

Eine erfolgreiche Antwort enthält eine [!UICONTROL Target-Bereitstellungs-API] Antwortobjekt, das vorab abgerufenen Inhalt für die angeforderten Mboxes enthält. Beispiel `targetResponse.response` -Objekt kann wie folgt aussehen:

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

Beachten Sie die mbox. `name` und `state` sowie die `eventToken` in jedem der [!DNL Target] Inhaltsoptionen. Diese sollten im `sendNotifications()` anfordern, sobald die einzelnen Inhaltsoptionen angezeigt werden. Nehmen wir einmal an, die `product1` Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

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

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token, das dem [!DNL Target] Angebot, das in der Vorabruf-Antwort bereitgestellt wird. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie an senden [!DNL Target] über die `sendNotifications()` API-Methode:

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
