---
title: Abonnieren von Ereignissen im  [!DNL Adobe Target] Python-SDK
description: Erfahren Sie, wie Sie mithilfe des Objekts [!UICONTROL OnDeviceDecisioningHandler] verschiedene Ereignisse abonnieren, die im Python-SDK auftreten.
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# SDK-Ereignisse (Python)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) ist das `options["events"]` -Attribut ein optionales Objekt mit Ereignisnamenschlüsseln und Callback-Funktionswerten. Sie kann zum Abonnieren verschiedener Ereignisse im SDK verwendet werden. Beispielsweise kann das `client_ready` -Ereignis mit einer Callback-Funktion verwendet werden, die aufgerufen wird, wenn das SDK für Methodenaufrufe bereit ist.

Wenn die Funktion `callback` aufgerufen wird, wird ein Ereignisobjekt übergeben. Jedes Ereignis hat einen `type` -Wert, der dem Ereignisnamen entspricht, und einige Ereignisse enthalten zusätzliche Eigenschaften mit relevanten Informationen.

## Ereignis- 

| Ereignisname (Typ) | Beschreibung | Zusätzliche Ereigniseigenschaften |
| --- | --- | --- |
| client_ready | Wird ausgegeben, wenn das Artefakt heruntergeladen wurde und das SDK für get_offer-Aufrufe bereit ist. Wird empfohlen bei Verwendung von | Entscheidungsmethode auf dem Gerät. | Keine |
| artifact_download_succeeded | Wird jedes Mal gesendet, wenn ein neues Artefakt heruntergeladen wird. | artifact_payload, artifact_location |
| artifact_download_failed | Wird jedes Mal gesendet, wenn ein Artefakt nicht heruntergeladen werden kann. | artifact_location, Fehler |

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
