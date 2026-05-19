---
title: Initialisieren der  [!DNL Adobe Target] -Python-SDK zum Protokollieren von Anforderungen
description: Erfahren Sie, wie Sie Anfragen in der  [!DNL Adobe Target] -SDK protokollieren.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
TQID: https://experienceleague.adobe.com/9LSln8V3QIG9GTok2yTTnKvhlpQhaed3a-qJyA4jErg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 3%

---

# Logger (Python)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) ist das `options["logger"]`-Objekt ein optionales Objekt. Standardmäßig wird unter dem Namespace `adobe.target` eine Protokollierung auf INFO-Ebene erstellt. Um jedoch die Protokollebene anzupassen oder effektiv zu debuggen, wenn ein Problem auftritt, kann bei der Initialisierung von SDK ein `logger` bereitgestellt werden.

Es wird erwartet, dass das `logger`-Objekt eine `debug()` und eine `error()` Methode aufweist. Wenn ein entsprechender Logger bereitgestellt wird, werden [!DNL Target] Anfragen und Antworten protokolliert.

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
