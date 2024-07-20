---
title: Erfahren Sie, wie Sie den benutzerdefinierten HTTP-Client konfigurieren
description: Erfahren Sie, wie Sie TargetClient mit ClientConfig.builder().httpClient() konfigurieren.
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Benutzerdefinierte HTTP-Client-Konfiguration (Java)

Wenn für die Anwendung, die das SDK ausführt, ein benutzerdefinierter HTTP-Client erforderlich ist, um Funktionen wie das Konfigurieren von SSL oder das Hinzufügen von Standardkopfzeilen zu Anforderungen zu aktivieren, muss der `TargetClient` mit `ClientConfig.builder().httpClient()` konfiguriert werden:

## Grundlegende benutzerdefinierte HTTP-Client-Konfiguration

Das SDK unterstützt derzeit HTTP-Clients, die die `org.apache.http.client.HttpClient` -Schnittstelle implementieren.

### Grundlegende Implementierung

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Benutzerdefinierte HTTP-Client-Konfiguration mit SSL-Konfiguration

Im Folgenden finden Sie ein Beispiel für die Konfiguration von SSL im `TargetClient` durch Anpassen des `HttpClient`, der an den `ClientConfig` übergeben wird. Das folgende Codefragment verwendet Klassen aus dem `org.apache.http.conn.ssl` -Paket für die SSL-Konfiguration.

### SSL-Implementierung

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
