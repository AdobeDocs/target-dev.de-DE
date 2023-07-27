---
title: Verwendung [!UICONTROL getOffers()] in [!DNL Adobe Target] bei Verwendung des Node.js-SDK
description: Verwendung von [!UICONTROL getOffers()] zum Ausführen einer Entscheidung und Abrufen eines Erlebnisses aus [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 22%

---

# [!UICONTROL Angebote abrufen] (Node.js)

## Beschreibung

`[!UICONTROL getOffers()]` wird zum Ausführen einer Entscheidung und zum Abrufen eines Erlebnisses aus verwendet [!DNL Adobe Target].


## Methode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parameter

Die `options` -Objekt weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- |--- | --- | --- | --- |
| Anfrage | Objekt | Ja | Keine | Entspricht dem [[!DNL Target] Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) Anfrage |
| visitorCookie | Zeichenfolge | Nein | Keine | ECID-Cookie (VisitorId) |
| targetCookie | Zeichenfolge | Nein | Keine | [!DNL Target] Cookie |
| targetLocationHint | Zeichenfolge | Nein | Keine | [!DNL Target] Standorthinweis |
| consumerId | Zeichenfolge | Nein | Keine | consumerIds für [!UICONTROL Analytics for Target] (A4T)-Stitching |
| CustomerIds | Array | Nein | Keine | Kunden-IDs im mit VisitorId kompatiblen Format |
| sessionId | Zeichenfolge | Nein | Keine | Dient zum Verknüpfen mehrerer [!DNL Target] requests |
| Besucher | Objekt | Nein | new VisitorId | Externe VisitorId-Instanz bereitstellen |

## Promise

`Promise` zurückgegeben weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | Objekt | [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) Anfrage |
| response | Objekt | [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) response |
| visitorState | Objekt | Objekt, das an die Besucher-API übergeben werden soll `getInstance()` |
| targetCookie | Objekt | [!DNL Target] Cookie |
| targetLocationHintCookie | Objekt | [!DNL Target] Standorthinweis-Cookie |
| analyticsDetails | Array | Analytics-Nutzlast bei clientseitiger Analytics-Nutzung |
| responseTokens | Array | Eine Liste von [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Array | Aggregierte Trace-Daten für alle Anfrage-Mboxes/Ansichten |
| status | Objekt | Ein Objekt, das den Status der Antwort enthält. |
| decisioningMethod | Zeichenfolge | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([auf Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), serverseitig, hybrid) |

`targetCookie` und `targetLocationHintCookie` -Objekte, die zum Zurückgeben von Daten an den Browser verwendet werden, weisen die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | Zeichenfolge | Cookie-Name |
| value | Alle | Cookie-Wert, wird in Zeichenfolge konvertiert. |
| maxAge | Nummer | Die `maxAge` ist eine praktische Option, um die Ablaufzeit relativ zur aktuellen Zeit in Sekunden festzulegen. |

Die `status` -Objekt zur Angabe des Status der Zielantwort weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| status | Nummer | HTTP-Statuscode |
| message | Zeichenfolge | Eine Meldung über die Antwort. Beispielsweise kann es darauf hinweisen, ob die Antwort entschieden wurde [auf Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) oder serverseitig |
| remoteMboxes | Array | Wenn die Entscheidungsmethode `on-device`, wird ein Array von Mbox-Namen angegeben, die nicht vollständig auf dem Gerät festgelegt werden konnten. Mit anderen Worten: ein [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) -Anfrage erforderlich. |

## Beispiel

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
