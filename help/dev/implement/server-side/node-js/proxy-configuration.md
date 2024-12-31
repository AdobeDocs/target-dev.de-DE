---
title: Implementieren der Proxy-Konfiguration in der  [!DNL Adobe Target] .js-SDK
description: Erfahren Sie, wie Sie die [!UICONTROL TargetClient]-Proxy-Konfiguration in der  [!DNL Adobe Target] .js-SDK konfigurieren.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Proxy-Konfiguration (Node.js)

Um einen Proxy für die HTTP-Anfragen des SDK-Knotens zu konfigurieren, überschreiben Sie die Abruf-API, die von der SDK während der Initialisierung verwendet wird.

Im Folgenden finden Sie ein einfaches Beispiel, das zeigt, wie `fetchApi` während der `TargetClient`-Initialisierung überschrieben werden können, um einen Proxy hinzuzufügen:

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

Beachten Sie, dass dies nur für Knotenversionen 18.2+ funktioniert, in denen `undici.fetch` der `fetch` für den Knoten ist.
Besuchen Sie das [Node SDK-Beispielrepo](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
Beispiele für die Proxy-Konfiguration für ältere Versionen des Knotens und weitere Informationen.
