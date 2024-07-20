---
title: Initialisieren des  [!DNL Adobe Target] Python-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen im  [!DNL Adobe Target] Python-SDK protokollieren.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) ist das `options["logger"]` -Objekt ein optionales Objekt. Standardmäßig wird eine INFO-Level-Logger unter dem Namespace `adobe.target` erstellt. Um jedoch die Protokollebene anzupassen oder beim Auftreten eines Problems effektiv zu debuggen, kann beim Initialisieren des SDK ein `logger` -Objekt bereitgestellt werden.

Es wird erwartet, dass das `logger` -Objekt eine `debug()` - und eine `error()` -Methode aufweist. Wenn eine entsprechende Protokollfunktion bereitgestellt wird, werden [!DNL Target] -Anfragen und -Antworten protokolliert.

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
