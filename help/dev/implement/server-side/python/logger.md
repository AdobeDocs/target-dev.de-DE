---
title: Initialisieren Sie die [!DNL Adobe Target] Python SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## Beschreibung

Wann [Initialisieren des SDK](initialize-sdk.md), die `options["logger"]` -Objekt ist ein optionales Objekt. Standardmäßig wird eine INFO-Level-Logger im `adobe.target` Namespace. Um jedoch die Protokollebene anzupassen oder eine effektive Fehlerbehebung durchzuführen, wenn ein Problem auftritt, muss ein `logger` -Objekt kann beim Initialisieren des SDK bereitgestellt werden.

Die `logger` -Objekt muss über eine `debug()` und `error()` -Methode. Wenn eine geeignete Protokollfunktion bereitgestellt wird, [!DNL Target] -Anfragen und -Antworten werden protokolliert.

## Beispiel

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

In der Konsole sollten Anforderungen und Antworten gedruckt werden.
