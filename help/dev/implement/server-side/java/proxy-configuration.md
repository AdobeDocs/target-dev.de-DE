---
title: Implementieren der Proxy-Konfiguration im [!DNL Adobe Target] Java-SDK
description: Erfahren Sie, wie Sie die TargetClient-Proxy-Konfiguration im [!DNL Adobe Target] Java-SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# Proxy-Konfiguration (Java)

## Grundlegender Proxy

Wenn für die Anwendung, die das SDK ausführt, ein Proxy für den Internetzugang erforderlich ist, muss die `TargetClient` mit einer Proxy-Konfiguration wie folgt konfiguriert werden.

### Grundlegende Proxy-Konfiguration

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Authentifizierung

Wenn eine Proxy-Authentifizierung erforderlich ist, können die Anmeldeinformationen als Parameter an die `ClientProxyConfig` -Konstruktor, wie im folgenden Beispiel gezeigt. Beachten Sie, dass dies nur für einfache Benutzername/Kennwort-Proxy-Authentifizierung funktioniert.

### Grundlegende Proxy-Authentifizierung

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
