---
title: Initialisieren des Python-SDK mit der create-Methode
description: Erfahren Sie, wie Sie die Methode create verwenden, um das Python-SDK zu initialisieren und die [!UICONTROL TargetClient] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 18%

---

# Initialisieren des Python-SDK

Beschreibung Verwenden Sie die `create` -Methode verwenden, um das Python-SDK zu initialisieren und die [!UICONTROL Target-Client] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.

## Methode

### erstellen

```python {line-numbers="true"}
TargetClient.create(options)
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| client | str | Ja | Keine | [!UICONTROL Adobe Target-Client-ID] |
| organization_id | str | Ja | Keine | [!UICONTROL Organisations-ID des Experience Cloud] |
| Zeitüberschreitung | int | Nein | 3000 | Zeitüberschreitung in Millisekunden |
| server_domain | str | Nein | `client.tt.omtrdc.net` |  | Überschreibt den standardmäßigen Hostnamen |
| secure | bool | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| Logger | Hauptobjekt umbenennen | Nein | INFO-Logger |  | Ersetzt den standardmäßigen INFO-Logger |
| target_location_hint | str | Nein | Keine | [!DNL Target] Standorthinweis |
| property_token | str | Nein | Keine | [!DNL Target] Property-Token. Wenn hier angegeben, verwenden alle Aufrufe von get_offer diesen Wert. |
| decisioning_method | str | Nein | serverseitig | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([auf Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), serverseitig, hybrid) |
| poling_interval | int | Nein | 300000 (5 Minuten) | Abrufintervall für die [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) in ms |
| artifact_location | str | Nein | Keine | Eine vollständig qualifizierte URL für die [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Überschreibt intern ermittelte Position. |
| artifact_payload | Hauptobjekt umbenennen | Nein | Keine | Die JSON-Payload der [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Wenn angegeben, wird sie anstelle einer Anforderung von einer URL verwendet. |
| [events](sdk-events.md) | dict &lt;str callable=&quot;&quot;> | Nein | Keine | Ein optionales Objekt mit Ereignisnamenschlüsseln und Callback-Funktionswerten |
| environment_id | int | Nein | production | Die [!DNL Target] Umgebungs-ID |
| Umgebung | str | Nein | production | Die [!DNL Target] Umgebungsname |
| cdn_environment | str | Nein | production | Name der CDN-Umgebung |
| telemetry_enabled | bool | Nein | True | Wenn der Wert auf &quot;False&quot;gesetzt ist, werden keine Telemetrikdaten an gesendet [!DNL Adobe] |
| version | str | Nein | Keine | Die Versionsnummer dieses SDK |

## Beispiel

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
