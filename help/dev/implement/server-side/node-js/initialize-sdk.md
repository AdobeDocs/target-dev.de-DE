---
title: Initialisieren Sie die Node.js-SDK mit der create-Methode
description: Erfahren Sie, wie Sie mit der create-Methode die Node.js-SDK initialisieren und den [!DNL Target]-Client instanziieren können, um Aufrufe an [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse durchzuführen.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
TQID: 'https://experienceleague.adobe.com/uawle0-l5bcv-FuXMLkPc8kIf8DvbkRqAYelr-ehNLk'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 17%
---
# Initialisieren der Node.js-SDK

## Beschreibung

Verwenden Sie die `create`-Methode, um die Node.js-SDK zu initialisieren und den [!UICONTROL Target]-Client zu instanziieren, sodass [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse aufgerufen wird.

## Methode

**Erstellen**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Kunde | Zeichenfolge | Ja | Keine | [!UICONTROL Adobe Target-Client-ID] |
| OrganizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Experience Cloud-Organisations-ID] |
| Umgebung | Zeichenfolge | Nein | Produktion | Name der Zielumgebung. Wählen Sie in der [!DNL Target]-Benutzeroberfläche [!UICONTROL Administration] > [!UICONTROL Umgebungen]. |
| Zeitüberschreitung | Nummer | Nein | 3000 | Timeout in Millisekunden |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den Standard-Host-Namen |
| sicher | Boolesch | Nein | wahr | Einstellung zur Durchsetzung des HTTP-Schemas |
| Holzfäller | Objekt | Nein | NOOP-Logger | Ersetzt den standardmäßigen NOOP-Logger |
| targetLocationHint | Zeichenfolge | Nein | Keine | Hinweis auf Zielort |
| fetchAPI | Funktion | Nein | global.fetch oder window.fetch | [fetch](https://fetch.spec.whatwg.org/) wird von SDK für HTTP-Anfragen verwendet. Standardmäßig wird node-fetch oder die Browser-Implementierung von fetch verwendet. Eine alternative Implementierung kann jedoch mithilfe von `fetchApi` bereitgestellt werden |
| propertyToken | Zeichenfolge | Nein | Keine | **Target-Eigenschaften-Token**. Wenn hier angegeben, verwenden alle `getOffers` diesen Wert. **Bei der geräteinternen** lädt die SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschaften-Token enthält, das in festgelegt `propertyToken` |
| decisioningMethod | Zeichenfolge | Nein | Server-seitig | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([geräteintern](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) Server-seitig, hybrid) |
| Abrufintervall | Nummer | Nein | 300000 (5 Minuten) | Abrufintervall für das [Artefakt der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in Millisekunden) |
| artifactLocation | Zeichenfolge | Nein | Keine | Eine vollständig qualifizierte URL zum [Artefakt der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Überschreibt den intern festgelegten Speicherort. |
| artifactPayload | Objekt | Nein | Keine | Die JSON-Payload des [Artefakts der geräteinternen Entscheidungsregel](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Wenn angegeben, wird sie verwendet, anstatt eine URL anzufordern. |
| [events](sdk-events.md) | Objekt&lt;Zeichenfolge, Funktion> | Nein | Keine | Ein optionales Objekt mit Ereignisnamenschlüsseln und Rückruffunktionswerten |
| telemetrisch aktiviert | Boolesch | Nein | wahr | Nach der Aktivierung erfasst Adobe Daten zur Nutzung von SDK-Funktionen und Leistungstelemetriedaten. Personenbezogene Daten werden nicht erfasst. |

## Beispiel

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
