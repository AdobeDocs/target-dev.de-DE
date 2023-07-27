---
title: Implementieren der Proxy-Konfiguration im [!DNL Adobe Target] Node.js-SDK
description: Erfahren Sie, wie Sie die [!UICONTROL TargetClient] Proxy-Konfiguration in der [!DNL Adobe Target] Node.js-SDK.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Proxy-Konfiguration (Node.js)

Um einen Proxy für die HTTP-Anfragen des Node SDK zu konfigurieren, überschreiben Sie die Abruf-API, die vom SDK während der Initialisierung verwendet wird.

Im Folgenden finden Sie ein grundlegendes Beispiel für die Außerkraftsetzung von `fetchApi` während der `TargetClient` Initialisierung zum Hinzufügen eines Proxys:

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Beachten Sie, dass dies nur für die Knotenversionen 18.2+ funktioniert, in denen `undici.fetch` ist der Standardwert `fetch` für Knoten.
Besuchen Sie die [Node SDK samples repo](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
für Beispiele zur Proxy-Konfiguration für ältere Versionen von Knoten und weitere Informationen.
