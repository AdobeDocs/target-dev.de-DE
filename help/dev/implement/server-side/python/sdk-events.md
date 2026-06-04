---
title: Abonnieren von Ereignissen in der  [!DNL Adobe Target] -SDK
description: Erfahren Sie, wie Sie verschiedene Ereignisse in Python SDK mit dem Objekt [!UICONTROL OnDeviceDecisioningHandler] abonnieren.
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
TQID: https://experienceleague.adobe.com/iFtlxw8Wlc9EMtDTndtXD7a2gu1TzGM6ijXire9gHPk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 166
ht-degree: 3%

---

# SDK-Ereignisse (Python)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) ist das `options["events"]`-dict ein optionales Objekt mit Ereignisnamenschlüsseln und Rückruffunktionswerten. Sie kann verwendet werden, um verschiedene Ereignisse zu abonnieren, die innerhalb der SDK auftreten. Beispielsweise kann das `client_ready`-Ereignis mit einer Rückruffunktion verwendet werden, die aufgerufen wird, wenn die SDK für Methodenaufrufe bereit ist.

Wenn die `callback` aufgerufen wird, wird ein Ereignisobjekt übergeben. Jedes Ereignis verfügt über einen `type`, der dem Ereignisnamen entspricht, und einige Ereignisse enthalten zusätzliche Eigenschaften mit relevanten Informationen.

## Ereignis-

| Ereignisname (Typ) | Beschreibung | Zusätzliche Ereigniseigenschaften |
| --- | --- | --- |
| client_ready | Wird ausgegeben, wenn das Artefakt heruntergeladen wurde und die SDK für get_offers-Aufrufe bereit ist. Wird bei Verwendung der geräteinternen Entscheidungsmethode empfohlen. | Keine |
| artifact_download_successful | Wird bei jedem Herunterladen eines neuen Artefakts ausgegeben. | artifact_payload, artifact_location |
| artifact_download_failed | Wird jedes Mal ausgegeben, wenn ein Artefakt nicht heruntergeladen werden kann. | artifact_location, Fehler |

## Beispiel

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
