---
title: Anzeigen- oder Klickbenachrichtigungen senden an [!DNL Adobe Target] Verwenden des Java-SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klickbenachrichtigungen an senden können. [!DNL Adobe Target] für die Messung und Berichterstellung.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 2%

---

# Benachrichtigungen senden (Java)

## Beschreibung

`sendNotifications()` wird verwendet, um Anzeigen- oder Klickbenachrichtigungen an zu senden [!DNL Adobe Target] für die Messung und Berichterstellung.

>[!NOTE]
>
>Wenn ein `execute` -Objekt mit erforderlichen Parametern in der Anfrage selbst enthalten ist, wird die Impression für qualifizierte Aktivitäten automatisch inkrementiert.

SDK-Methoden, die eine Impression automatisch erhöhen, sind:

* `getOffers()`
* `getAttributes()`

Wenn eine `prefetch` -Objekt innerhalb der Anfrage übergeben wird, wird die Impression nicht automatisch für die Aktivitäten mit Mboxes innerhalb der `prefetch` -Objekt. `sendNotifications()` muss für vorab abgerufene Erlebnisse zur Erhöhung von Impressionen und Konversionen verwendet werden.

## Methode

### erstellen

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## Beispiel

Erstellen wir zunächst die [!DNL Target Delivery API] Anfrage zum Vorabruf von Inhalten für die `home` und `product1` Mboxes verwenden.

### Vorabruf

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

Eine erfolgreiche Antwort enthält eine [!UICONTROL Target-Bereitstellungs-API] Antwortobjekt, das vorab abgerufenen Inhalt für die angeforderten Mboxes enthält. Beispiel `targetResponse.response` -Objekt kann wie folgt aussehen:

### Antwort

```javascript {line-numbers="true"}
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

Beachten Sie die mbox. `name` und `state` sowie die `eventToken` in jedem der [!DNL Target] Inhaltsoptionen. Diese sollten im `sendNotifications()` anfordern, sobald die einzelnen Inhaltsoptionen angezeigt werden. Nehmen wir einmal an, die `product1` Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage sieht wie folgt aus:

### Anfrage

```javascript {line-numbers="true"}
TargetDeliveryRequest mboxNotificationRequest = TargetDeliveryRequest.builder().notifications(new ArrayList() {{
    add(new Notification()
            .id("1")
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox()
                    .name("product1")
                    .state("J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
            )
            .tokens(Arrays.asList(new String[]{"t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="}))
    );
}}).build();
```

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token, das dem [!DNL Target] Angebot, das in der Vorabruf-Antwort bereitgestellt wird. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie an senden [!DNL Target] via `sendNotifications()` API-Methode:

### Antwort

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
