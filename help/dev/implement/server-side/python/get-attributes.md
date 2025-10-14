---
title: Verwenden asynchroner Anfragen in der Python [!DNL Adobe Target] SDK
description: Erfahren Sie [!DNL Target]  wie Python SDK asynchrone Anforderungen unterstützt, wodurch die effektive Zielzeit auf null reduziert werden kann.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 16%

---

# Attribute abrufen (Python)

## Beschreibung

`get_attributes()` wird verwendet, um Experimente und personalisierte Erlebnisse aus [!DNL Target] abzurufen und Attributwerte zu extrahieren.


## Methode

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Parameter

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | Ja | Keine | Eine Liste von Mbox-Namen |
| options | verordnen | Nein | Keine | Die gleichen Optionen wie für &quot;[&quot; &#x200B;](get-offers.md) |

## AttributesProvider

Die von `target_client.get_attributes()` zurückgegebene `AttributesProvider` weist die folgenden Methoden auf:

| Methode | Rückgabetyp | Beschreibung |
| --- | --- | --- |
| get_value(mbox_name, key) | any | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| as_object(mbox_name) | verordnen | Gibt ein einfaches JSON-Objekt mit Schlüsselwertpaaren zurück. |
| get_response() | [targetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | Gibt das Antwortobjekt zurück, das normalerweise von `get_offers` zurückgegeben wird |

## Beispiel

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
