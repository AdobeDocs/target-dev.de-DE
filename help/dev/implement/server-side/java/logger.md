---
title: Initialisieren der  [!DNL Adobe Target] -Java-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen in der Java [!DNL Adobe Target] SDK protokollieren.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
TQID: https://experienceleague.adobe.com/xvduuV6cjVJu-yIoaxCvbPE-ZttfEViuM8B7sVczAC0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 4%

---

# Logger (Java)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) gibt es mehrere Optionen für das `ClientConfig`-Objekt, die auf Protokollanfragen festgelegt werden können.

| Option | Beschreibung |
| --- | --- |
| `logRequests` | Protokolliert den gesamten Anfragetext sowie den Antworttext. |
| `logRequestStatus` | Protokolliert die URL der Anfrage, den Status zusammen mit der Antwortzeit. |

[!DNL Target] Java SDK verwendet die `slf4j`. Sie müssen die Implementierung von Logger bereitstellen, z. B. `java.util.logging`, `logback` und `log4j`. Weitere Informationen finden Sie ](https://www.slf4j.org/manual.html) [https://www.slf4j.org/manual.html. Alle Protokolle werden in `debug` gedruckt.

## Beispiel

Fügen Sie die `slf4j` hinzu.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Aktivieren Sie die `DEBUG` basierend auf Ihrer Implementierung und markieren Sie die Flags für die Anfrageprotokollierung.

### Debug

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

In der Konsole sollten Anforderungen, Antworten und Antwortzeiten gedruckt werden.
