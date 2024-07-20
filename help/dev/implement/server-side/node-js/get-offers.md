---
title: Verwenden Sie [!UICONTROL getOffers()] in  [!DNL Adobe Target]  bei der Verwendung des Node.js-SDK.
description: Erfahren Sie, wie Sie mit [!UICONTROL getOffers()] eine Entscheidung ausführen und ein Erlebnis aus  [!DNL Adobe Target] abrufen können.
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 22%

---

# [!UICONTROL Get Offers] (Node.js)

## Beschreibung

`[!UICONTROL getOffers()]` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.


## Methode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parameter

Das Objekt `options` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- |--- | --- | --- | --- |
| Anfrage | Objekt | Ja | Keine | Entspricht der Anforderung für die [[!DNL Target] Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) |
| visitorCookie | Zeichenfolge | Nein | Keine | ECID-Cookie (VisitorId) |
| targetCookie | Zeichenfolge | Nein | Keine | [!DNL Target] -Cookie |
| targetLocationHint | Zeichenfolge | Nein | Keine | [!DNL Target] Standorthinweis |
| consumerId | Zeichenfolge | Nein | Keine | consumerIds für das Stitching von [!UICONTROL Analytics for Target] (A4T) |
| CustomerIds | Array | Nein | Keine | Kunden-IDs im mit VisitorId kompatiblen Format |
| sessionId | Zeichenfolge | Nein | Keine | Wird zum Verknüpfen mehrerer [!DNL Target] -Anforderungen verwendet |
| Besucher | Objekt | Nein | new VisitorId | Externe VisitorId-Instanz bereitstellen |

## Promise

`Promise` zurückgegeben hat die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | Objekt | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) Anfrage |
| response | Objekt | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) Antwort |
| visitorState | Objekt | Objekt, das an die Besucher-API `getInstance()` übergeben werden soll |
| targetCookie | Objekt | [!DNL Target] -Cookie |
| targetLocationHintCookie | Objekt | [!DNL Target] location hint cookie |
| analyticsDetails | Array | Analytics-Nutzlast bei clientseitiger Analytics-Nutzung |
| responseTokens | Array | Eine Liste mit [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Array | Aggregierte Trace-Daten für alle Anfrage-Mboxes/Ansichten |
| status | Objekt | Ein Objekt, das den Status der Antwort enthält. |
| decisioningMethod | Zeichenfolge | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), serverseitig, hybrid) |

Die Objekte `targetCookie` und `targetLocationHintCookie`, die zum Zurückgeben von Daten an den Browser verwendet werden, weisen die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | Zeichenfolge | Cookie-Name |
| value | Alle | Cookie-Wert, wird in Zeichenfolge konvertiert. |
| maxAge | Nummer | Die Option &quot;`maxAge`&quot; ist eine praktische Option, mit der die Zeitdauer in Sekunden relativ zur aktuellen Zeit abläuft |

Das `status` -Objekt, das zur Angabe des Status der Zielantwort verwendet wird, weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| status | Nummer | HTTP-Statuscode |
| message | Zeichenfolge | Eine Meldung über die Antwort. Beispielsweise kann es darauf hinweisen, ob die Antwort auf [auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) oder serverseitig entschieden wurde |
| remoteMboxes | Array | Wenn die Entscheidungsmethode &quot;`on-device`&quot; lautet, wird ein Array von Mbox-Namen angegeben, über die auf dem Gerät nicht vollständig entschieden werden konnte. Anders ausgedrückt: Es ist eine [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) -Anfrage erforderlich. |

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
