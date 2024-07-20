---
title: Initialisieren des Java-SDK [!DNL Adobe Target] zur Protokollierung von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im Java-SDK [!DNL Adobe Target] protokollieren.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Logger (Java)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) gibt es mehrere Optionen für das Objekt `ClientConfig`, die auf Protokollanforderungen festgelegt werden können.

| Option | Beschreibung |
| --- | --- |
| `logRequests` | Protokolliert den gesamten Anforderungstext sowie den Antworttext. |
| `logRequestStatus` | Protokolliert die URL der Anfrage, den Status sowie die Antwortzeit. |

[!DNL Target] Java SDK verwendet die `slf4j` -Protokollierung. Sie müssen Ihre Implementierung der Protokollfunktion bereitstellen, z. B. `java.util.logging`, `logback` und `log4j`. Weitere Informationen finden Sie unter [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) . Alle Protokolle werden in `debug` gedruckt.

## Beispiel

Fügen Sie die `slf4j` -Abhängigkeit hinzu.

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

Aktivieren Sie die `DEBUG` -Protokolle basierend auf Ihrer Implementierung und markieren Sie die Protokollierungsmarkierungen der Anforderungen.

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

Sie sollten sehen, wie Anfragen, Antworten und Antwortzeiten in der Konsole gedruckt werden.
