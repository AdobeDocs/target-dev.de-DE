---
title: Vorabruf der Adobe Target-Bereitstellungs-API
description: Wie verwende ich den Vorabruf im [!UICONTROL Adobe Target-Bereitstellungs-API]?
keywords: Versandschnittstelle
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 9a3068b0765c238daa2f9af904c0f6f15b57cc24
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Vorabruf

Durch den Vorabruf können Clients wie mobile Apps und Server Inhalte für mehrere Mboxes oder Ansichten in einer Anfrage abrufen, lokal zwischenspeichern und später benachrichtigen [!DNL Target] wenn der Benutzer diese Mboxes oder Ansichten besucht.

Bei der Verwendung des Vorabrufs ist es wichtig, mit den folgenden Begriffen vertraut zu sein:

| Feldname | Beschreibung |
| --- | --- |
| `prefetch` | Liste der Mboxes und Ansichten, die abgerufen, aber nicht als besucht markiert werden sollten. Die [!DNL Target] Edge gibt eine `eventToke`n für jede Mbox oder Ansicht, die im Vorabruf-Array vorhanden sind. |
| `notifications` | Liste der mboxes und Ansichten, die zuvor vorabgerufen wurden und als besucht markiert werden sollen. |
| `eventToken` | Ein Hash-verschlüsseltes Token, das zurückgegeben wird, wenn Inhalt vorab abgerufen wird. Dieses Token sollte zurück an [!DNL Target] im `notifications` Array. |

## Vorabruf-mboxes

Clients wie mobile Apps und Server können mehrere Mboxes für einen bestimmten Benutzer in einer Sitzung vorab abrufen und zwischenspeichern, um mehrere Aufrufe an zu vermeiden [!UICONTROL Adobe Target-Bereitstellungs-API].

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
  "id": {
    "tntId": "abcdefghijkl00023.1_1"
  },
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
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

Innerhalb der `prefetch` -Feld ein oder mehrere `mboxes` Sie möchten für einen Benutzer in einer Sitzung gleichzeitig vorab abrufen. Sobald Sie diese `mboxes` Sie erhalten die folgende Antwort:

```
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

In der Antwort sehen Sie die `content` -Feld, das das Erlebnis enthält, das dem Benutzer für eine bestimmte `mbox`. Dies ist sehr nützlich, wenn sie auf Ihrem Server zwischengespeichert wird, sodass, wenn ein Benutzer innerhalb einer Sitzung mit Ihrer Web- oder Mobile-App interagiert und eine `mbox` auf einer bestimmten Seite Ihrer Anwendung kann das Erlebnis aus dem Cache bereitgestellt werden, anstatt eine andere [!UICONTROL Adobe Target-Bereitstellungs-API] aufrufen. Wenn dem Benutzer jedoch ein Erlebnis von der `mbox`, a `notification` wird über einen Versand-API-Aufruf gesendet, damit die Impressions-Protokollierung erfolgt. Dies liegt an der Antwort von `prefetch` -Aufrufe zwischengespeichert werden. Das bedeutet, dass der Benutzer die Erlebnisse zum Zeitpunkt der `prefetch` -Aufruf erfolgt. Um mehr über die `notification` Prozess, siehe [Benachrichtigungen](notifications.md).

## Vorabruf-mboxes mit ClickTrack-Metriken bei Verwendung von [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics für Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T) ist eine lösungsübergreifende Integration, mit der Sie Aktivitäten basierend auf [!DNL Analytics] Konversionsmetriken und Zielgruppensegmente.

Das folgende Codefragment ist eine Antwort aus einem Vorabruf einer Mbox, die `clickTrack` Zu benachrichtigende Metriken [!DNL Analytics] dass auf ein Angebot geklickt wurde:

```
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>Der Vorabruf für eine Mbox enthält die [!DNL Analytics] Nutzlast nur für qualifizierte Aktivitäten. Das Vorabrufen von Erfolgsmetriken für noch nicht qualifizierte Aktivitäten führt zu Inkonsistenzen bei der Berichterstellung.

## Ansichten vorab abrufen

Ansichten unterstützen Single Page Applications (SPA) und Mobile Apps nahtloser. Ansichten können als logische Gruppe visueller Elemente betrachtet werden, aus denen ein SPA oder ein mobiles Erlebnis besteht. Über die Bereitstellungs-API erstellte VEC jetzt AB- und XT-Aktivitäten mit Änderungen in [Ansichten für SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) kann jetzt vorabgerufen werden.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

Der obige Beispielaufruf ruft alle Ansichten, die über den SPA VEC für AB- und XT-Aktivitäten erstellt wurden, für die Anzeige im Internet vor `channel`. Beachten Sie im -Aufruf, dass wir alle Ansichten aus den AB- oder XT-Aktivitäten abrufen möchten, mit denen ein Besucher `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` der die `url`:`https://target.enablementadobe.com/react/demo/#/` qualifiziert.

```
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

Im `content` Felder der Antwort, Notiz-Metadaten wie `type`, `selector`, `cssSelector`, und `content`, die zum Rendern des Erlebnisses für Ihren Endbenutzer verwendet werden, wenn ein Benutzer Ihre Seite besucht. Beachten Sie Folgendes: `prefetched` Inhalte können bei Bedarf zwischengespeichert und für den Benutzer gerendert werden.
