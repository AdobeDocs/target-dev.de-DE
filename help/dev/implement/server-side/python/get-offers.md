---
title: Verwenden Sie getOffers() in [!DNL Adobe Target] bei Verwendung des Python SDK
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis abrufen können aus [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 13%

---

# Angebote abrufen (Python)

## Beschreibung

`get_offers()` wird zum Ausführen einer Entscheidung und zum Abrufen eines Erlebnisses aus verwendet [!DNL Adobe Target].


## Methode

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Parameter

Die `options` dict weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Anfrage | DeliveryRequest | Ja | Keine | Entspricht dem [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) Anfrage |
| target_cookie | str | no | Keine | [!DNL Target] Cookie |
| target_location_hint | str | no | Keine | [!DNL Target] Standorthinweis |
| consumer_id | str | no | Keine | Beim Zuordnen mehrerer Aufrufe sollten unterschiedliche Kunden-IDs angegeben werden |
| customer_ids | Liste[CustomerId] | no | Keine | Eine Liste der Kunden-IDs im mit VisitorId kompatiblen Format |
| session_id | str | no | Keine | Wird zum Verknüpfen mehrerer Anforderungen verwendet |
| callback | callable | no | Keine | Wenn die Anfrage asynchron verarbeitet wird, wird der Callback aufgerufen, wenn die Antwort bereit ist |
| err_callback | callable | no | Keine | Wenn die Anfrage asynchron verarbeitet wird, wird beim Auslösen einer Ausnahme der Fehler-Callback aufgerufen |

## Rückgabe

Gibt eine `TargetDeliveryResponse` wenn synchron aufgerufen wird (Standard) oder eine `AsyncResult` , wenn mit einem Rückruf aufgerufen wird. `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| response | DeliveryResponse | Entspricht dem [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) response |
| target_cookie | dict | [!DNL Target] Cookie |
| target_location_hint_cookie | dict | [!DNL Target] Standorthinweis-Cookie |
| analytics_details | Liste[AnalyticsResponse] | Analytics-Nutzlast bei clientseitiger Analytics-Nutzung |
| trace | Liste[dict] | Aggregierte Trace-Daten für alle Anfrage-Mboxes/Ansichten |
| response_tokens | Liste[dict] | Liste der &#x200B;[Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| Meta | dict | Zusätzliche Entscheidungsmetadaten für die Verwendung mit on-device-Decisioning |

`target_cookie` und `target_location_hint_cookie` -Objekte, die zum Zurückgeben von Daten an den Browser verwendet werden, weisen die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | str | Cookie-Name |
| value | any | Cookie-Wert, wird der Wert in eine Zeichenfolge konvertiert |
| max_age | int | Die `max_age option` ist eine einfache Möglichkeit, das Festlegen von Läuft relativ zur aktuellen Zeit in Sekunden vorzunehmen |

Die `meta` -Objekt zur Angabe des Status der Zielantwort weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| decisioning_method | str | Welche Entscheidungsmethode wurde verwendet: auf dem Gerät oder serverseitig |
| remote_mboxes | befindet`[str]` | Wenn die Entscheidungsmethode `on-device`, wird ein Array von Mbox-Namen angegeben, die nicht vollständig auf dem Gerät festgelegt werden konnten. Mit anderen Worten: ein [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) -Anfrage erforderlich. |
| remote_views | befindet`[str]` | Wenn die Entscheidungsmethode auf dem Gerät ausgeführt wird, wird ein Array von Ansichtsnamen angegeben, die nicht vollständig auf dem Gerät festgelegt werden konnten. Mit anderen Worten: ein [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) -Anfrage erforderlich. |

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
