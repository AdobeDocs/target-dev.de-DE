---
title: Benutzerberechtigungen für Adobe Target Delivery API
description: Benutzerberechtigungen für Adobe Target Delivery API
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Erfahren Sie, was in Target Premium enthalten ist."
keywords: Versandschnittstelle
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Benutzerberechtigungen (Premium)

Mit [!DNL Adobe] können Kunden bei der Verwendung von Adobe Target Benutzerberechtigungen verwalten. Um einen erfolgreichen [!UICONTROL Adobe Target Delivery API] -Aufruf durchzuführen, muss ein Token mit den richtigen Berechtigungen innerhalb des API-Aufrufs übergeben werden. Um mehr über die Benutzerberechtigungen und das Abrufen des Tokens zu erfahren, besuchen Sie [diese Dokumentation](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

Sobald Sie über das entsprechende Token verfügen, übergeben Sie es für jeden API-Aufruf an `property` -> `token`. Wenn die `property` -> `token` nicht bei jedem API-Aufruf übergeben wird, erhalten Sie keine `content` zurück von Adobe Target.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

Wie Sie oben sehen können, ohne die `property` -> `token` zu übergeben, erhalten Sie keine Inhalte zurück. Wenn Sie Inhalte von Ihrem API-Aufruf erwarten, aber keine aus der Antwort abrufen, liegt das wahrscheinlich daran, dass entweder `property` -> `token` nicht bereitgestellt wird oder dass es ohne die richtigen Berechtigungen weitergegeben wird.
