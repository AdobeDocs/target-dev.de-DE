---
title: Adobe Target-Bereitstellungs-API - Erste Schritte
description: Wie verwende ich die [!UICONTROL Adobe Target Delivery API]?
keywords: Bereitstellungs-API
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Erste Schritte mit dem [!UICONTROL Adobe Target Delivery API]

Ein [!UICONTROL Target Delivery API] Aufruf sieht wie folgt aus:

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

Die `clientCode` können über die [!DNL Target]-Benutzeroberfläche abgerufen werden, indem Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** navigieren.

Bevor Sie einen [!UICONTROL Target Delivery API]-Aufruf ausführen, führen Sie die folgenden Schritte aus, um sicherzustellen, dass eine Antwort das relevante Erlebnis enthält, um Endbenutzenden zu zeigen:

1. Erstellen Sie eine [!DNL Target] Aktivität (A/B, XT, AP oder Recommendations) mit dem [formularbasierten Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de) oder dem [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de).
1. Verwenden Sie die Bereitstellungs-API, um eine Antwort für die Mboxes zu erhalten, die in der in Schritt 2 erstellten [!DNL Target]-Aktivität verwendet werden.
1. Präsentieren Sie dem Besucher das Erlebnis.
