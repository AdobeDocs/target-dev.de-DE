---
title: Initialisieren des Node.js-SDK mit der Methode create
description: Erfahren Sie, wie Sie mit der Methode create das Node.js-SDK initialisieren und die [!DNL Target] Client zum Aufrufen an [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 18%

---

# Initialisieren des Node.js-SDK

## Beschreibung

Verwenden Sie die `create` -Methode verwenden, um das Node.js-SDK zu initialisieren und die [!UICONTROL Target] Client zum Aufrufen an [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.

## Methode

**erstellen**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parameter

`options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| client | Zeichenfolge | Ja | Keine | [!UICONTROL Adobe Target Client ID] |
| organizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Organisations-ID des Experience Cloud] |
| Umgebung | Zeichenfolge | Nein | production | Name der Zielumgebung. Im [!DNL Target] Benutzeroberfläche, [!UICONTROL Administration] > [!UICONTROL Umgebungen]. |
| Zeitüberschreitung | Nummer | Nein | 3000 | Zeitüberschreitung in Millisekunden |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den standardmäßigen Hostnamen |
| secure | Boolesch | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| Logger | Objekt | Nein | NOOP Logger | Ersetzt den standardmäßigen NOOP-Logger |
| targetLocationHint | Zeichenfolge | Nein | Keine | Target-Standorthinweis |
| fetchAPI | Funktion | Nein | global.fetch oder window.fetch | [abrufen](https://fetch.spec.whatwg.org/) wird vom SDK für HTTP-Anfragen verwendet. Standardmäßig wird node-fetch oder die Browserimplementierung des Abrufs verwendet. Eine alternative Implementierung kann jedoch mit `fetchApi` |
| propertyToken | Zeichenfolge | Nein | Keine | **Target-Eigenschafts-Token**. Wenn hier angegeben, werden alle `getOffers` -Aufrufe verwenden diesen Wert. **Für geräteübergreifende Entscheidungen**, lädt das SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschafts-Token enthält, das in `propertyToken` |
| decisioningMethod | Zeichenfolge | Nein | serverseitig | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([auf Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), serverseitig, hybrid) |
| ollingInterval | Nummer | Nein | 300000 (5 Minuten) | Abrufintervall für die [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in Millisekunden) |
| artifactLocation | Zeichenfolge | Nein | Keine | Eine vollständig qualifizierte URL für die [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Überschreibt intern ermittelte Position. |
| artifactPayload | Objekt | Nein | Keine | Die JSON-Payload der [Artefakt der Entscheidungsregel auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Wenn angegeben, wird sie anstelle einer Anforderung von einer URL verwendet. |
| [events](sdk-events.md) | Objekt&lt;string function=&quot;&quot;> | Nein | Keine | Ein optionales Objekt mit Ereignisnamenschlüsseln und Callback-Funktionswerten |
| telemetryEnabled | Boolesch | Nein | wahr | Wenn diese Option aktiviert ist, erfasst Adobe die Nutzung von SDK-Funktionen und Leistungstelemetrikdaten. Personenbezogene Daten werden nicht erfasst. |

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
