---
title: Anzeigen- oder Klickbenachrichtigungen senden an [!DNL Adobe Target] Verwenden des Python-SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klickbenachrichtigungen an senden können. [!DNL Adobe Target] für die Messung und Berichterstellung.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 8%

---

# Benachrichtigungen senden (Python)

## Beschreibung

`send_notifications()` wird verwendet, um Anzeigen- oder Klickbenachrichtigungen an zu senden [!DNL Adobe Target] für die Messung und Berichterstellung.

>[!NOTE]
>
>Wenn ein `execute` -Objekt mit erforderlichen Parametern in der Anfrage selbst enthalten ist, wird die Impression für qualifizierte Aktivitäten automatisch inkrementiert.

SDK-Methoden, die eine Impression automatisch erhöhen, sind:

* `get_offers()`
* `get_attributes()`

Wenn eine `prefetch` -Objekt innerhalb der Anfrage übergeben wird, wird die Impression nicht automatisch für die Aktivitäten mit Mboxes innerhalb der `prefetch` -Objekt. `Send_notifications()` muss für vorab abgerufene Erlebnisse zur Erhöhung von Impressionen und Konversionen verwendet werden.

## Methode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Anfrage | DeliveryRequest | Ja | Keine | Entspricht dem [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) Anfrage |
| target_cookie | str | no | Keine | [!DNL Target] Cookie |
| target_location_hint | str | no | Keine | [!DNL Target] Standorthinweis |
| consumer_id | str | no | Keine | Beim Zuordnen mehrerer Aufrufe sollten unterschiedliche Kunden-IDs angegeben werden |
| customer_ids | Liste[CustomerId] | no | Keine | Eine Liste der Kunden-IDs im mit VisitorId kompatiblen Format |
| session_id | str | no | Keine | Wird zum Verknüpfen mehrerer Anforderungen verwendet |
| callback | callable | no | Keine | Wenn die Anfrage asynchron verarbeitet wird, wird der Callback aufgerufen, wenn die Antwort bereit ist |
| err_callback | callable | no | Keine | Wenn die Anfrage asynchron verarbeitet wird, wird beim Auslösen einer Ausnahme der Fehler-Callback aufgerufen |

## Rückgabe

`Returns` a `TargetDeliveryResponse` wenn synchron aufgerufen wird (Standard) oder eine `AsyncResult` , wenn mit einem Rückruf aufgerufen wird. `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| response | DeliveryResponse | Entspricht dem [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) response |
| target_cookie | dict | [!DNL Target] Cookie |
| target_location_hint_cookie | dict | [!DNL Target] Standorthinweis-Cookie |
| analytics_details | Liste[AnalyticsResponse] | [!DNL Analytics] Nutzlast bei clientseitiger [!DNL Analytics] usage |
| trace |  | Liste[dict] | Aggregierte Trace-Daten für alle Anfrage-Mboxes/Ansichten |
| response_tokens | Liste[dict] | Eine Liste von [&#x200B; Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| Meta | dict | Zusätzliche Entscheidungsmetadaten für die Verwendung mit on-device-Decisioning |

## Beispiel

Erstellen wir zunächst die [!UICONTROL Target-Bereitstellungs-API] Anfrage zum Vorabruf von Inhalten für die `home` und `product1` Mboxes verwenden.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Eine erfolgreiche Antwort enthält eine [!UICONTROL Target-Bereitstellungs-API] Antwortobjekt, das vorab abgerufenen Inhalt für die angeforderten Mboxes enthält. Beispiel `target_response["response"]` -Objekt (formatiert als Dict) kann wie folgt aussehen:

### Python

```python {line-numbers="true"}
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

Beachten Sie die mbox. `name` und `state` sowie die `eventToken` in den einzelnen Target-Inhaltsoptionen. Diese sollten im `send_notifications()` anfordern, sobald die einzelnen Inhaltsoptionen angezeigt werden. Nehmen wir einmal an, die `product1` Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token, das dem [!DNL Target] Angebot, das in der Vorabruf-Antwort bereitgestellt wird. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie an senden [!DNL Target] über die `send_notifications()` API-Methode:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
