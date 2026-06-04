---
title: Adobe Target-Bereitstellungs-API - Erste Schritte
description: Wie verwende ich die [!UICONTROL Adobe Target-Bereitstellungs-]?
keywords: Bereitstellungs-API
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 1%

---

# Erste Schritte mit der [!UICONTROL Adobe Target-Bereitstellungs-API]

Ein [!UICONTROL Target-Bereitstellungs]API-Aufruf sieht wie folgt aus:

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

Die `clientCode` können über die [!DNL Target]-Benutzeroberfläche abgerufen werden, indem Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** navigieren.

Bevor Sie einen Aufruf [!UICONTROL Target-Bereitstellungs-API] durchführen, führen Sie die folgenden Schritte aus, um sicherzustellen, dass eine Antwort das relevante Erlebnis für die Endbenutzerinnen und -benutzer enthält:

1. Erstellen Sie eine [!DNL Target] Aktivität (A/B, XT, AP oder Recommendations) mit dem [formularbasierten Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) oder dem [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Verwenden Sie die Bereitstellungs-API, um eine Antwort für die Mboxes zu erhalten, die in der in Schritt 2 erstellten [!DNL Target]-Aktivität verwendet werden.
1. Präsentieren Sie dem Besucher das Erlebnis.
