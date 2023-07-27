---
title: Adobe Target-Bereitstellungs-API - Erste Schritte
description: Wie verwende ich die [!UICONTROL Adobe Target-Bereitstellungs-API]?
keywords: Versandschnittstelle
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Erste Schritte mit dem [!UICONTROL Adobe Target-Bereitstellungs-API]

A [!UICONTROL Target-Bereitstellungs-API] -Aufruf sieht wie folgt aus:

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

Die `clientCode` kann aus der [!DNL Target] Benutzeroberfläche durch Navigieren zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.

Bevor Sie [!UICONTROL Target-Bereitstellungs-API] aufrufen, führen Sie die folgenden Schritte aus, um sicherzustellen, dass eine Antwort das relevante Erlebnis enthält, um Endbenutzer anzuzeigen:

1. Erstellen Sie eine [!DNL Target] -Aktivität (A/B, XT, AP oder Recommendations), die die [Formularbasierter Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) oder [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. Verwenden Sie die Bereitstellungs-API, um eine Antwort für die Mboxes zu erhalten, die in der [!DNL Target] Aktivität, die in Schritt 2 erstellt wurde.
1. Präsentieren Sie das Erlebnis dem Besucher.

## Postman-Sammlung {#postman}

Postman ist eine Anwendung, die das Auslösen von API-Aufrufen erleichtert. [Diese Postman-Sammlung](https://run.pstmn.io/button.svg) enthält Beispiel-Bereitstellungs-API-Aufrufe.
