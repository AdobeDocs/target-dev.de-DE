---
title: Verwenden von getOffers() in  [!DNL Adobe Target]  bei Verwendung der Python-SDK
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis aus abrufen können [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---

# Abrufen von Angeboten (Python)

## Beschreibung

`get_offers()` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.


## Methode

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Parameter

Das `options` hat die folgende Struktur:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Anfrage | Versandanfrage | Ja | Keine | Entspricht der [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | no | Keine | Cookie [!DNL Target] |
| target_location_hint | str | no | Keine | [!DNL Target] Standorthinweis |
| consumer_id | str | no | Keine | Beim Zusammenfügen mehrerer Aufrufe sollten verschiedene Verbraucher-IDs angegeben werden |
| customer_ids | list[CustomerId] | no | Keine | Eine Liste der Kunden-IDs im VisitorId-kompatiblen Format |
| session_id | str | no | Keine | Wird zum Verknüpfen mehrerer Anfragen verwendet |
| callback | kündbar | no | Keine | Wenn eine Anfrage asynchron verarbeitet wird, wird der Callback aufgerufen, wenn die Antwort bereit ist |
| err_callback | kündbar | no | Keine | Wenn eine Anfrage asynchron verarbeitet wird, wird beim Auslösen einer Ausnahme ein Fehler-Rückruf aufgerufen |

## Rückgaben

Gibt einen `TargetDeliveryResponse` zurück, wenn synchron aufgerufen (Standard), oder einen `AsyncResult`, wenn er mit einem Callback aufgerufen wird. `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Antwort | deliveryResponse | Entspricht der [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) Antwort |
| target_cookie | verordnen | Cookie [!DNL Target] |
| target_location_hint_cookie | verordnen | Cookie für [!DNL Target]-Standorthinweise |
| analytics_details | list[analyticsResponse] | Analytics-Payload im Fall einer Client-seitigen Analytics-Nutzung |
| Spur | list[dict] | Aggregierte Trace-Daten für alle Anfrage-Mboxes/-Ansichten |
| response_token | list[dict] | Eine Liste von &#x200B;[Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | verordnen | Zusätzliche Entscheidungsmetadaten zur Verwendung mit der geräteinternen Entscheidungsfindung |

`target_cookie` - und `target_location_hint_cookie` -Objekte, die für die Rückgabe von Daten an den Browser verwendet werden, haben die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | str | Cookie-Name |
| value | any | Cookie-Wert, der Wert wird in eine Zeichenfolge konvertiert |
| max_age | int | Die `max_age option` ist praktisch, wenn die Einstellung relativ zur aktuellen Zeit in Sekunden abläuft |

Das `meta` -Objekt, das zur Anzeige des Status der Zielantwort verwendet wird, hat die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| decisioning_method | str | Welche Entscheidungsmethode verwendet wurde: On-Device oder Server-seitig |
| remote_mboxes | `[str]` | Wenn die Entscheidungsmethode `on-device` wird, wird ein Array von Mbox-Namen angegeben, über die auf dem Gerät nicht vollständig entschieden werden konnte. Mit anderen Worten, es ist eine [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) erforderlich. |
| remote_views | `[str]` | Wenn die Entscheidungsmethode auf dem Gerät ist, wird ein Array von Ansichtsnamen angegeben, über die auf dem Gerät nicht vollständig entschieden werden konnte. Mit anderen Worten, es ist eine [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) erforderlich. |

## Beispiel

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
