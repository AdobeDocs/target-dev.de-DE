---
title: Initialisieren des [!DNL Adobe Target] Node.js-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im SDK [!DNL Adobe Target] Node.js protokollieren.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Logger (Node.js)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) ist das `options.logger` -Objekt ein optionales Objekt. Um jedoch effektiv zu debuggen, wenn ein Problem auftritt, sollte bei der Initialisierung des SDK ein `logger` -Objekt bereitgestellt werden.

Es wird erwartet, dass das `logger` -Objekt eine `debug()` - und eine `error()` -Methode aufweist. Wenn eine entsprechende Protokollfunktion bereitgestellt wird, z. B. `console`, werden [!DNL Target] -Anfragen und -Antworten protokolliert.

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
