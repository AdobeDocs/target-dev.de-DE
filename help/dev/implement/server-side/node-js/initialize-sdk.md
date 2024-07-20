---
title: Initialisieren des Node.js-SDK mit der Methode create
description: Erfahren Sie, wie Sie mit der create -Methode das Node.js-SDK initialisieren und den  [!DNL Target] Client instanziieren, um Aufrufe an  [!DNL Adobe Target]  für Experimente und personalisierte Erlebnisse durchzuführen.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 19%

---

# Initialisieren des Node.js-SDK

## Beschreibung

Verwenden Sie die `create` -Methode, um das Node.js-SDK zu initialisieren und den [!UICONTROL Target]-Client zu instanziieren, um für Experimente und personalisierte Erlebnisse Aufrufe an [!DNL Adobe Target] durchzuführen.

## Methode

**create**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| client | Zeichenfolge | Ja | Keine | [!UICONTROL Adobe Target Client ID] |
| organizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Experience Cloud Organization ID] |
| Umgebung | Zeichenfolge | Nein | production | Name der Zielumgebung. In der Benutzeroberfläche von [!DNL Target] ist [!UICONTROL Administration] > [!UICONTROL Environments]. |
| Zeitüberschreitung | Nummer | Nein | 3000 | Zeitüberschreitung in Millisekunden |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den standardmäßigen Hostnamen |
| secure | Boolesch | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| Logger | Objekt | Nein | NOOP Logger | Ersetzt den standardmäßigen NOOP-Logger |
| targetLocationHint | Zeichenfolge | Nein | Keine | Target-Standorthinweis |
| fetchAPI | Funktion | Nein | global.fetch oder window.fetch | [fetch](https://fetch.spec.whatwg.org/) wird vom SDK für HTTP-Anfragen verwendet. Standardmäßig wird node-fetch oder die Browserimplementierung des Abrufs verwendet. Eine alternative Implementierung kann jedoch mit `fetchApi` bereitgestellt werden |
| propertyToken | Zeichenfolge | Nein | Keine | **Target-Eigenschafts-Token**. Wenn hier angegeben, verwenden alle `getOffers` -Aufrufe diesen Wert. **Für Entscheidungen auf dem Gerät** lädt das SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschaft-Token enthält, das in `propertyToken` festgelegt ist. |
| decisioningMethod | Zeichenfolge | Nein | serverseitig | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), serverseitig, hybrid) |
| ollingInterval | Nummer | Nein | 300000 (5 Minuten) | Abrufintervall für das [on-device decisioning rule artifact](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in Millisekunden) |
| artifactLocation | Zeichenfolge | Nein | Keine | Eine vollständig qualifizierte URL für das [auf dem Gerät vorhandene Entscheidungsregel-Artefakt](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Überschreibt intern ermittelte Position. |
| artifactPayload | Objekt | Nein | Keine | Die JSON-Payload des [auf dem Gerät befindlichen Entscheidungsregel-Artefakts](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Wenn angegeben, wird sie anstelle einer Anforderung von einer URL verwendet. |
| [events](sdk-events.md) | Object&lt;String,Function> | Nein | Keine | Ein optionales Objekt mit Ereignisnamenschlüsseln und Callback-Funktionswerten |
| telemetryEnabled | Boolesch | Nein | wahr | Wenn diese Option aktiviert ist, erfasst Adobe SDK-Funktionsnutzung und Leistungstelemetrikdaten. Personenbezogene Daten werden nicht erfasst. |

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
