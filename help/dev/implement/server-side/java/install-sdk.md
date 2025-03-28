---
title: Installieren der Java-SDK
description: Erfahren Sie, wie Sie die Java [!DNL Adobe Target] SDK installieren.
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Installieren der Java-SDK

Die Java-SDK wird von [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk) verteilt. Fügen Sie zunächst eine Abhängigkeit hinzu, indem Sie in `gradle` oder `maven` installieren:

>[!BEGINTABS]

>[!TAB Gradle]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

Den Open-Source-Code finden Sie unter <https://github.com/adobe/target-java-sdk>.
