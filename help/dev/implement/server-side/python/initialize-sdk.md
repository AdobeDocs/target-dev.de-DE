---
title: Initialisieren von Python SDK mithilfe der create-Methode
description: Erfahren Sie, wie Sie mit der create-Methode die Python-SDK initialisieren und die [!UICONTROL TargetClient] instanziieren können, um  [!DNL Adobe Target]  Experimente und personalisierte Erlebnisse aufzurufen.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 17%

---

# Initialisieren von Python SDK

Beschreibung
Verwenden Sie die `create`-Methode, um die Python-SDK zu initialisieren und die [!UICONTROL Target Client] zu instanziieren und [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse aufzurufen.

## Methode

### erstellen

```python {line-numbers="true"}
TargetClient.create(options)
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Kunde | str | Ja | Keine | [!UICONTROL Adobe Target client ID] |
| ORGANIZATION_ID | str | Ja | Keine | [!UICONTROL Experience Cloud Organization ID] |
| Zeitüberschreitung | int | Nein | 3000 | Timeout in Millisekunden |
| server_domain | str | Nein | `client.tt.omtrdc.net` | Überschreibt den Standard-Host-Namen |
| sicher | boolesch | Nein | wahr | Einstellung zur Durchsetzung des HTTP-Schemas |
| Holzfäller | Objekt | Nein | INFO-Logger | Ersetzt den standardmäßigen INFO-Logger |
| target_location_hint | str | Nein | Keine | [!DNL Target] Standorthinweis |
| property_token | str | Nein | Keine | [!DNL Target]-Eigenschafts-Token Wenn hier angegeben, verwenden alle get_offers-Aufrufe diesen Wert. |
| decisioning_method | str | Nein | Server-seitig | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([geräteintern](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) Server-seitig, hybrid) |
| polling_interval | int | Nein | 300000 (5 Minuten) | Abrufintervall für das [Artefakt der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in ms) |
| artifact_location | str | Nein | Keine | Eine vollständig qualifizierte URL zum [Artefakt der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Überschreibt den intern festgelegten Speicherort. |
| artifact_payload | Objekt | Nein | Keine | Die JSON-Payload des [Artefakts der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Wenn angegeben, wird sie verwendet, anstatt eine URL anzufordern. |
| [events](sdk-events.md) | dict &lt;str, callable> | Nein | Keine | Ein optionales Objekt mit Ereignisnamenschlüsseln und Rückruffunktionswerten |
| environment_id | int | Nein | Produktion | Die ID der [!DNL Target] Umgebung |
| Umgebung | str | Nein | Produktion | Der Name der [!DNL Target] |
| cdn_environment | str | Nein | Produktion | Der Name der CDN-Umgebung |
| telemetry_enabled | boolesch | Nein | True | Bei der Einstellung „False“ werden keine Telemetriedaten an [!DNL Adobe] gesendet |
| version | str | Nein | Keine | Die Versionsnummer dieser SDK |

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
