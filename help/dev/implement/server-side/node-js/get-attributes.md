---
title: Verwendung asynchroner Anforderungen in der [!DNL Adobe Target] Node.js-SDK
description: Erfahren Sie mehr [!DNL Target] Das Node.js-SDK unterstützt asynchrone Anforderungen, wodurch die effektive Zielzeit auf null reduziert werden kann.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# Abrufen von Attributen (Node.js)

## Beschreibung

`[!UICONTROL getAttributes()]` wird zum Abrufen von Experimenten und personalisierten Erlebnissen aus [!DNL Target] und extrahieren Sie Attributwerte.

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

Die `Promise` zurückgegeben `TargetClient.getAttributes()` löst ein Objekt mit den folgenden Methoden auf:

| Methode | Rückgabetyp | Beschreibung |
| --- | --- | --- |
| getValue(mboxName, key) | Alle | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| asObject(mboxName) | Objekt | Gibt ein einfaches JSON-Objekt mit Schlüsselwertpaaren zurück |
| getResponse() | [getOffers-Antwort](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Gibt das Antwortobjekt zurück, das normalerweise von `getOffers` |

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
