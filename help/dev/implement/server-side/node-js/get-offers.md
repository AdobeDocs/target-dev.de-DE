---
title: Verwenden [!UICONTROL getOffers()] in [!DNL Adobe Target] bei Verwendung der Node.js-SDK
description: Erfahren Sie, wie Sie [!UICONTROL getOffers()] verwenden, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
TQID: 'https://experienceleague.adobe.com/WRGy74F1kUobRl1Pakse0VnXt3cT3-ntCljm4bHtiZ4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 20%
---
# [!UICONTROL Angebote abrufen] (Node.js)

## Beschreibung

`[!UICONTROL getOffers()]` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.


## Methode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parameter

Das `options`-Objekt hat die folgende Struktur:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- |--- | --- | --- | --- |
| Anfrage | Objekt | Ja | Keine | Entspricht der Anfrage [[!DNL Target] Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) |
| visitorCookie | Zeichenfolge | Nein | Keine | ECID-Cookie (VisitorId) |
| targetCookie | Zeichenfolge | Nein | Keine | Cookie [!DNL Target] |
| targetLocationHint | Zeichenfolge | Nein | Keine | [!DNL Target] Standorthinweis |
| consumerId | Zeichenfolge | Nein | Keine | consumerIds für das [!UICONTROL Analytics for Target] (A4T)-Stitching |
| Kunden-IDs | Array | Nein | Keine | Kunden-IDs im VisitorId-kompatiblen Format |
| sessionId | Zeichenfolge | Nein | Keine | Wird zum Verknüpfen mehrerer [!DNL Target] verwendet |
| Besucher | Objekt | Nein | new VisitorId | Externe VisitorId-Instanz bereitstellen |

## Versprechen

`Promise` zurückgegebene weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | Objekt | [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) Anfrage |
| Antwort | Objekt | [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md) Antwort |
| visitorState | Objekt | Objekt, das an die Besucher-API-`getInstance()` übergeben werden soll |
| targetCookie | Objekt | Cookie [!DNL Target] |
| targetLocationHintCookie | Objekt | Cookie für [!DNL Target]-Standorthinweise |
| analyticsDetails | Array | Analytics-Payload im Fall einer Client-seitigen Analytics-Nutzung |
| responseTokens | Array | Eine Liste von [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de&). |
| Spur | Array | Aggregierte Trace-Daten für alle Anfrage-Mboxes/-Ansichten |
| status | Objekt | Ein Objekt, das den Status der Antwort enthält. |
| decisioningMethod | Zeichenfolge | Bestimmt, welche Entscheidungsmethode verwendet werden soll ([geräteintern](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) Server-seitig, hybrid) |

`targetCookie` - und `targetLocationHintCookie` -Objekte, die für die Rückgabe von Daten an den Browser verwendet werden, haben die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | Zeichenfolge | Cookie-Name |
| value | Alle | Cookie-Wert, wird der in eine Zeichenfolge umgewandelt |
| maxAge | Nummer | Die Option `maxAge` ist eine praktische Option, um festzulegen, dass die Gültigkeit relativ zur aktuellen Zeit in Sekunden abläuft |

Das `status` -Objekt, das zur Anzeige des Status der Zielantwort verwendet wird, hat die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| status | Nummer | HTTP-Status-Code |
| message | Zeichenfolge | Eine Meldung zur Antwort. Beispielsweise kann es angeben, ob die Antwort [On-Device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) oder Server-seitig festgelegt wurde |
| remoteMboxes | Array | Wenn die Entscheidungsmethode `on-device` wird, wird ein Array von Mbox-Namen angegeben, über die auf dem Gerät nicht vollständig entschieden werden konnte. Mit anderen Worten, eine [[!UICONTROL Target-Bereitstellungs-API]](/help/dev/implement/delivery-api/overview.md)-Anfrage ist erforderlich. |

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
