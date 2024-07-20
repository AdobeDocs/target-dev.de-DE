---
title: Verwendung asynchroner Anforderungen im SDK [!DNL Adobe Target] Node.js
description: Erfahren Sie, wie das [!DNL Target] Node.js-SDK asynchrone Anfragen unterstützt, wodurch die effektive Zielzeit auf null reduziert werden kann.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 18%

---

# Abrufen von Attributen (Node.js)

## Beschreibung

`[!UICONTROL getAttributes()]` wird verwendet, um Experimente und personalisierte Erlebnisse aus [!DNL Target] abzurufen und Attributwerte zu extrahieren.

## Methode

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Parameter

| Name | Typ | Erforderlich | Standardeinstellung |
| --- | --- | --- |--- |
| mboxNames | Array | Ja | Keine |
| options | Objekt | Nein | Keine |

## Promise

Mit dem von `TargetClient.getAttributes()` zurückgegebenen `Promise` wird ein Objekt mit den folgenden Methoden aufgelöst:

| Methode | Rückgabetyp | Beschreibung |
| --- | --- | --- |
| getValue(mboxName, key) | Alle | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| asObject(mboxName) | Objekt | Gibt ein einfaches JSON-Objekt mit Schlüsselwertpaaren zurück |
| getResponse() | [getOffers response](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Gibt das Antwortobjekt zurück, das normalerweise von `getOffers` zurückgegeben wird |

## Beispiel

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
