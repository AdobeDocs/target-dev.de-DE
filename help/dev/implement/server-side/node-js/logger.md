---
title: Initialisieren der  [!DNL Adobe Target] .js-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen in der SDK  [!DNL Adobe Target] Node.js“ protokollieren.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
TQID: https://experienceleague.adobe.com/tC6xT-eAHOO17h1BK-PwWTBmwg3Dy0Wj8KYrV3W-VR4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 83
ht-degree: 2%

---

# Logger (Node.js)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) ist das `options.logger`-Objekt ein optionales Objekt. Um jedoch effektiv debuggen zu können, wenn ein Problem auftritt, sollte beim Initialisieren der SDK ein `logger` bereitgestellt werden.

Es wird erwartet, dass das `logger`-Objekt eine `debug()` und eine `error()` Methode aufweist. Wenn ein entsprechender Logger bereitgestellt wird, z. B. `console`, werden [!DNL Target] Anfragen und Antworten protokolliert.

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
