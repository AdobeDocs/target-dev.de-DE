---
title: Anzeigen- oder Klickbenachrichtigungen senden an [!DNL Adobe Target] Verwenden des .NET SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klickbenachrichtigungen an senden können. [!DNL Adobe Target] für die Messung und Berichterstellung.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# Benachrichtigungen senden (.NET)

## Beschreibung

`SendNotifications()` wird verwendet, um Anzeigen- oder Klickbenachrichtigungen an zu senden [!DNL Adobe Target] für die Messung und Berichterstellung.

>[!NOTE]
>
>Wenn ein `Execute` -Objekt mit erforderlichen Parametern in der Anfrage selbst enthalten ist, wird die Impression für qualifizierte Aktivitäten automatisch inkrementiert.

SDK-Methoden, die eine Impression automatisch erhöhen, sind:

* `GetOffers()`
* `GetAttributes()`

Wenn eine `Prefetch` -Objekt innerhalb der Anfrage übergeben wird, wird die Impression nicht automatisch für die Aktivitäten mit Mboxes innerhalb der `Prefetch` -Objekt. `SendNotifications()` muss für vorab abgerufene Erlebnisse zur Erhöhung von Impressionen und Konversionen verwendet werden.

## Methode

### Erstellung 

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Beispiel

Erstellen wir zunächst die [!UICONTROL Target-Bereitstellungs-API] Anfrage zum Vorabruf von Inhalten für die `home` und `product1` Mboxes verwenden.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

Eine erfolgreiche Antwort enthält eine [!DNL Target Delivery API] Antwortobjekt, das vorab abgerufenen Inhalt für die angeforderten Mboxes enthält. Beispiel `targetResponse.Response` -Objekt kann wie folgt aussehen:

### \.NET

```dotnet {line-numbers="true"}
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

Beachten Sie die `mbox` Name und `state` sowie die `eventToken` in jedem der [!DNL Target] Inhaltsoptionen. Diese sollten im `SendNotifications()` anfordern, sobald die einzelnen Inhaltsoptionen angezeigt werden. Nehmen wir einmal an, die `product1` Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token, das dem [!DNL Target] Angebot, das in der Vorabruf-Antwort bereitgestellt wird. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie an senden [!DNL Target] über die `SendNotifications()` API-Methode:

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
