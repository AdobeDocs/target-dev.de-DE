---
title: Senden von Anzeige- oder Klickbenachrichtigungen an  [!DNL Adobe Target] mithilfe der Python-SDK
description: Erfahren Sie, wie Sie mit sendNotifications() Anzeigen- oder Klick-Benachrichtigungen an senden können [!DNL Adobe Target]  um Messungen und Berichte durchzuführen.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# Benachrichtigungen senden (Python)

## Beschreibung

`send_notifications()` wird verwendet, um Anzeige- oder Klick-Benachrichtigungen zur Messung und Berichterstellung an [!DNL Adobe Target] zu senden.

>[!NOTE]
>
>Wenn sich ein `execute` mit erforderlichen Parametern in der Anfrage selbst befindet, wird die Impression automatisch für qualifizierte Aktivitäten inkrementiert.

SDK-Methoden, die eine Impression automatisch inkrementieren:

* `get_offers()`
* `get_attributes()`

Wenn ein `prefetch` innerhalb der Anfrage übergeben wird, wird die Impression für die Aktivitäten mit Mboxes innerhalb des `prefetch`-Objekts nicht automatisch inkrementiert. `Send_notifications()` müssen für vorab abgerufene Erlebnisse verwendet werden, um Impressionen und Konversionen zu erhöhen.

## Methode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Anfrage | Versandanfrage | Ja | Keine | Entspricht der [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | no | Keine | Cookie [!DNL Target] |
| target_location_hint | str | no | Keine | [!DNL Target] Standorthinweis |
| consumer_id | str | no | Keine | Beim Zusammenfügen mehrerer Aufrufe sollten verschiedene Verbraucher-IDs angegeben werden |
| customer_ids | list[CustomerId] | no | Keine | Eine Liste der Kunden-IDs im VisitorId-kompatiblen Format |
| session_id | str | no | Keine | Wird zum Verknüpfen mehrerer Anfragen verwendet |
| callback | kündbar | no | Keine | Wenn eine Anfrage asynchron verarbeitet wird, wird der Callback aufgerufen, wenn die Antwort bereit ist |
| err_callback | kündbar | no | Keine | Wenn eine Anfrage asynchron verarbeitet wird, wird beim Auslösen einer Ausnahme ein Fehler-Rückruf aufgerufen |

## Rückgaben

`Returns` ein `TargetDeliveryResponse`, wenn synchron aufgerufen (Standard), oder ein `AsyncResult`, wenn mit einem Callback aufgerufen. `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Antwort | deliveryResponse | Entspricht der [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) Antwort |
| target_cookie | verordnen | Cookie [!DNL Target] |
| target_location_hint_cookie | verordnen | Cookie für [!DNL Target]-Standorthinweise |
| analytics_details | list[analyticsResponse] | [!DNL Analytics] Payload im Falle einer Client-seitigen [!DNL Analytics] |
| Spur | list[dict] | Aggregierte Trace-Daten für alle Anfrage-Mboxes/-Ansichten |
| response_token | list[dict] | Eine Liste von [&#x200B;Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de) |
| meta | verordnen | Zusätzliche Entscheidungsmetadaten zur Verwendung mit der geräteinternen Entscheidungsfindung |

## Beispiel

Erstellen wir zunächst die [!UICONTROL Target Delivery API] Anfrage zum Vorabrufen von Inhalten für die `home`- und `product1`-Mboxes.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Eine erfolgreiche Antwort enthält ein [!UICONTROL Target Delivery API] Antwortobjekt, das vorab abgerufene Inhalte für die angeforderten Mboxes enthält. Ein Beispielobjekt `target_response["response"]` (formatiert als dict) kann wie folgt aussehen:

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

Beachten Sie die Mbox-`name` und `state` Felder sowie das `eventToken` Feld in jeder der Target-Inhaltsoptionen. Diese sollten in der `send_notifications()`-Anfrage angegeben werden, sobald jede Inhaltsoption angezeigt wird. Angenommen, die `product1`-Mbox wurde auf einem Nicht-Browser-Gerät angezeigt. Die Benachrichtigungsanfrage wird wie folgt angezeigt:

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

Beachten Sie, dass wir sowohl den Mbox-Status als auch das Ereignis-Token entsprechend dem [!DNL Target] Angebot in der Prefetch-Antwort eingeschlossen haben. Nachdem wir die Benachrichtigungsanfrage erstellt haben, können wir sie über die [!DNL Target]-API-Methode an `send_notifications()` senden:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
