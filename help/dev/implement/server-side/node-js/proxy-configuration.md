---
title: Implementieren der Proxy-Konfiguration in der [!DNL Adobe Target] Node.js-SDK
description: Erfahren Sie, wie Sie die [!UICONTROL TargetClient]-Proxy-Konfiguration in der [!DNL Adobe Target] Node.js-SDK konfigurieren.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
TQID: 'https://experienceleague.adobe.com/kaE-ZEOTteaVp5kWSHiVYCvEiHuQHSMqeWRq6r-mJaA'
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
source-wordcount: '100'
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
