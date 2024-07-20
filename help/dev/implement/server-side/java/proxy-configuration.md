---
title: Proxy-Konfiguration im [!DNL Adobe Target] Java-SDK implementieren
description: Erfahren Sie, wie Sie die TargetClient-Proxy-Konfiguration im Java SDK [!DNL Adobe Target] konfigurieren.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
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

Wenn eine Proxy-Authentifizierung erforderlich ist, können die Anmeldeinformationen gemäß dem folgenden Beispiel als Parameter an den `ClientProxyConfig` -Konstruktor übergeben werden. Beachten Sie, dass dies nur für einfache Benutzername/Kennwort-Proxy-Authentifizierung funktioniert.

### Grundlegende Proxy-Authentifizierung

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Geräteinterne Entscheidungsfindung

Für Anfragen zum Abrufen des Regelartefakts sollte Ihr Proxy so konfiguriert sein, dass die Antwort nicht zwischengespeichert wird. Wenn es jedoch nicht möglich ist, den Cache-Mechanismus des Proxys für diese Anforderung zu konfigurieren, verwenden Sie eine Konfigurationsoption als Problemumgehung, um den Cache auf Proxyebene zu umgehen. Diese Problemumgehung fügt die Kopfzeile `Authorization` mit einem leeren Zeichenfolgenwert zur Regelanforderung hinzu, was dem Proxy anzeigen sollte, dass die Antwort nicht zwischengespeichert werden soll.

Um diese Problemumgehung zu aktivieren, legen Sie Folgendes fest:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


