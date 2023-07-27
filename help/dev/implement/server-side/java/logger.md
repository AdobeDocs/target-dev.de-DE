---
title: Initialisieren Sie die [!DNL Adobe Target] Java-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im [!DNL Adobe Target] Java-SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Logger (Java)

## Beschreibung

Wann [Initialisieren des SDK](initialize-sdk.md), gibt es mehrere Optionen auf der `ClientConfig` -Objekt, das auf Protokollanforderungen festgelegt werden kann.

| Option | Beschreibung |
| --- | --- |
| `logRequests` | Protokolliert den gesamten Anforderungstext sowie den Antworttext. |
| `logRequestStatus` | Protokolliert die URL der Anfrage, den Status sowie die Antwortzeit. |

[!DNL Target] Java SDK verwendet `slf4j` Protokollierung. Sie müssen Ihre Implementierung der Protokollfunktion bereitstellen, z. B. `java.util.logging`, `logback`, und `log4j`. Siehe Abschnitt [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) für weitere Informationen. Alle Protokolle werden ausgedruckt in `debug`.

## Beispiel

Fügen Sie die `slf4j` Abhängigkeit.

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

Aktivieren Sie die `DEBUG` Protokolle auf Grundlage Ihrer Implementierung erstellen und die Protokollierungsmarkierungen der Anforderungen markieren.

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
