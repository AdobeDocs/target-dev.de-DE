---
title: Implementieren der Proxy-Konfiguration in der  [!DNL Adobe Target] -Java-SDK
description: Erfahren Sie, wie Sie die TargetClient-Proxy-Konfiguration in der Java [!DNL Adobe Target] SDK konfigurieren.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Proxy-Konfiguration (Java)

## Basic Proxy

Wenn die Anwendung, die die SDK ausführt, einen Proxy benötigt, um auf das Internet zuzugreifen, muss die `TargetClient` wie folgt mit einer Proxy-Konfiguration konfiguriert werden.

### Einfache Proxy-Konfiguration

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Authentifizierung

Wenn eine Proxy-Authentifizierung erforderlich ist, können die Anmeldeinformationen als Parameter an den `ClientProxyConfig`-Konstruktor übergeben werden, wie im folgenden Beispiel dargestellt. Beachten Sie, dass dies nur für die einfache Benutzername/Kennwort-Proxy-Authentifizierung funktioniert.

### Einfache Proxy-Authentifizierung

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Geräteinterne Entscheidungsfindung

Für Anfragen zum Abrufen des Regelartefakts sollte Ihr Proxy so konfiguriert sein, dass die Antwort nicht zwischengespeichert wird. Wenn es jedoch nicht möglich ist, den Caching-Mechanismus des Proxys für diese Anfrage zu konfigurieren, verwenden Sie eine Konfigurationsoption als Problemumgehung, um den Cache auf Proxy-Ebene zu umgehen. Diese Problemumgehung fügt der Regelanforderung den `Authorization`-Header mit einem leeren Zeichenfolgenwert hinzu, der dem Proxy angeben sollte, dass die Antwort nicht zwischengespeichert werden soll.

Um diese Problemumgehung zu aktivieren, legen Sie Folgendes fest:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


