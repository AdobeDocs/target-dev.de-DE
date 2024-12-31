---
title: Senden von Anzeige- oder Klickbenachrichtigungen an [!DNL Adobe Target] mithilfe von .NET SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klick-Benachrichtigungen an senden können [!DNL Adobe Target]  um Messungen und Berichte durchzuführen.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Benachrichtigungen senden (.NET)

## Beschreibung

`SendNotifications()` wird verwendet, um Anzeige- oder Klick-Benachrichtigungen zur Messung und Berichterstellung an [!DNL Adobe Target] zu senden.

>[!NOTE]
>
>Wenn sich ein `Execute` mit erforderlichen Parametern in der Anfrage selbst befindet, wird die Impression automatisch für qualifizierte Aktivitäten inkrementiert.

SDK-Methoden, die eine Impression automatisch inkrementieren:

* `GetOffers()`
* `GetAttributes()`

Wenn ein `Prefetch` innerhalb der Anfrage übergeben wird, wird die Impression für die Aktivitäten mit Mboxes innerhalb des `Prefetch`-Objekts nicht automatisch inkrementiert. `SendNotifications()` müssen für vorab abgerufene Erlebnisse verwendet werden, um Impressionen und Konversionen zu erhöhen.

## Methode

### Erstellung 

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Beispiel

Erstellen wir zunächst die [!UICONTROL Target Delivery API] Anfrage zum Vorabrufen von Inhalten für die `home`- und `product1`-Mboxes.

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

Eine erfolgreiche Antwort enthält ein [!DNL Target Delivery API] Antwortobjekt, das vorab abgerufene Inhalte für die angeforderten Mboxes enthält. Ein Beispiel für ein `targetResponse.Response` kann wie folgt aussehen:

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

Beachten Sie die Felder `mbox` und `state` sowie das Feld `eventToken` in jeder der [!DNL Target] Inhaltsoptionen. Diese sollten in der `SendNotifications()`-Anfrage angegeben werden, sobald jede Inhaltsoption angezeigt wird. Angenommen, die `product1`-Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

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

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token entsprechend dem [!DNL Target] Angebot in der Prefetch-Antwort eingeschlossen haben. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie über die `SendNotifications()`-API-Methode an [!DNL Target] senden:

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
