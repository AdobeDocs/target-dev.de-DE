---
title: Initialisieren Sie die [!DNL Adobe Target] Node.js-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im [!DNL Adobe Target] Node.js-SDK.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Logger (Node.js)

## Beschreibung

Wann [Initialisieren des SDK](initialize-sdk.md), die `options.logger` -Objekt ist ein optionales Objekt. Um jedoch wirksam zu debuggen, wenn ein Problem auftritt, muss ein `logger` -Objekt sollte beim Initialisieren des SDK bereitgestellt werden.

Die `logger` -Objekt muss über eine `debug()` und `error()` -Methode. Wenn eine geeignete Protokollfunktion bereitgestellt wird, z. B. `console`, [!DNL Target] -Anfragen und -Antworten werden protokolliert.

## Beispiel

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

In der Konsole sollten Anforderungen und Antworten gedruckt werden.
