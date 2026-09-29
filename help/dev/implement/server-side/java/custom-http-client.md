---
title: Erfahren Sie, wie Sie den benutzerdefinierten HTTP-Client konfigurieren
description: Erfahren Sie, wie Sie TargetClient mithilfe von ClientConfig.builder().httpClient() konfigurieren.
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
TQID: 'https://experienceleague.adobe.com/SwijRIrhqSG4Mlij4sBH9Kx8tRB-6Bo7eyMoUZREOW8'
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
source-wordcount: '108'
ht-degree: 0%
---
# Benutzerdefinierte HTTP-Client-Konfiguration (Java)

Wenn die Anwendung, die die SDK ausführt, einen benutzerdefinierten HTTP-Client benötigt, um Funktionen wie die Konfiguration von SSL oder das Hinzufügen von Standardkopfzeilen zu Anfragen zu aktivieren, muss die `TargetClient` mithilfe von konfiguriert werden`ClientConfig.builder().httpClient()`:

## Grundlegende benutzerdefinierte HTTP-Client-Konfiguration

SDK unterstützt derzeit HTTP-Clients, die die `org.apache.http.client.HttpClient` implementieren.

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

Im Folgenden finden Sie ein Beispiel für die Konfiguration von SSL im `TargetClient` durch Anpassen der an den `ClientConfig` übergebenen `HttpClient`. Das folgende Codefragment verwendet Klassen aus dem `org.apache.http.conn.ssl` für die SSL-Konfiguration.

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
