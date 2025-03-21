---
title: Integration mit Experience Cloud
description: Integration mit Experience Cloud
keywords: Bereitstellungs-API
source-git-commit: f16903556954d2b1854acd429f60fbf6fc2920de
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Integration mit Experience Cloud

## Adobe Analytics for Target (A4T)

Wenn ein Aufruf der Target-Bereitstellungs-API vom Server ausgelöst wird, gibt Adobe Target das Erlebnis für diesen Benutzer zurück. Darüber hinaus gibt Adobe Target entweder die Adobe Analytics-Payload an den Aufrufer zurück oder leitet sie automatisch an Adobe Analytics weiter. Um Target-Aktivitätsinformationen Server-seitig an Adobe Analytics zu senden, müssen einige Voraussetzungen erfüllt sein:

1. Die Aktivität wird in der Adobe Target-Benutzeroberfläche mit Adobe Analytics als Berichtsquelle eingerichtet und die Konten sind für A4T aktiviert
1. Die Adobe Marketing Cloud-Besucher-ID wird vom API-Benutzer generiert und ist verfügbar, wenn der Target-Bereitstellungs-API-Aufruf ausgelöst wird

### Adobe Target leitet die Analytics-Payload automatisch weiter

Adobe Target kann die Analytics-Payload automatisch über die Serverseite an Adobe Analytics weiterleiten, wenn die folgenden Kennungen bereitgestellt werden:

1. `supplementalDataId` : Die ID, die für die Zuordnung zwischen Adobe Analytics und Adobe Target verwendet wird
1. `trackingServer`: Der Adobe-Analytics-Server Damit Adobe Target und Adobe Analytics die Daten korrekt zusammenfügen können, müssen dieselben `supplementalDataId` sowohl an Adobe Target als auch an Adobe Analytics übergeben werden.

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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
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

### Analytics-Payload von Adobe Target abrufen

Nutzerinnen und Nutzer der Adobe Target-Bereitstellungs-API können die Adobe Analytics-Payload für eine entsprechende Mbox abrufen, damit die Nutzerinnen und Nutzer die Payload über die [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) an Adobe Analytics senden können. Wenn ein Server-seitiger Adobe Target-Aufruf ausgelöst wird, übergeben Sie in der Anfrage `client_side` an das Feld `logging` . Dadurch wird wiederum eine Payload zurückgegeben, wenn die Mbox in einer Aktivität vorhanden ist, die Analytics als Berichtsquelle verwendet.

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
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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

Nachdem Sie `logging` = `client_side` angegeben haben, erhalten Sie die Payload im Feld `mbox` wie unten dargestellt.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                        "type": "html",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                        "type": "html",
                    }
                ]
            }
        ]
    }
}
```

Wenn die Target-Antwort etwas in der `payload` `analytics` -> enthält, leiten Sie es wie gewünscht an Adobe Analytics weiter. Analytics weiß, wie diese Payload verarbeitet wird. Dies kann in einer GET-Anfrage im folgenden Format erfolgen:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Parameter und Variablen von Abfragezeichenfolgen

| Feldname | Erforderlich | Beschreibung |
| --- | --- | --- |
| `rsid` | Ja | Die Report Suite-ID |
| `pe` | Ja | Seitenereignis. Immer auf `tnt` gesetzt |
| `tnta` | Ja | Analytics-Payload, die vom Target-Server in `analytics` -> `payload` -> `tnta` zurückgegeben wird |
| `mid` | Marketing Cloud-Besucher-ID |

### Erforderliche Kopfzeilenwerte

| Header-Name | Header-Wert |
| --- | --- |
| Host | Analytics-Datenerfassungs-Server (z. B.: adobeags421.sc.omtrdc.net) |

### HTTP-GET-Aufruf zum Einfügen von Beispiel-A4T-Daten

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Adobe Audience Manager (AAM)-Segmente können auch über Adobe Target-Bereitstellungs-APIs genutzt werden. Um AAM-Segmente nutzen zu können, müssen die folgenden Felder bereitgestellt werden:

| Feldname | Erforderlich | Beschreibung |
| --- | --- | --- |
| `locationHint` | Ja | Mit dem DCS-Standorthinweis wird bestimmt, welcher AAM-DCS-Endpunkt aufgerufen werden muss, um das Profil abzurufen. Muss >= 1 sein. |
| `marketingCloudVisitorId` | Ja | Marketing Cloud-Besucher-ID |
| `blob` | Ja | AAM Blob wird verwendet, um zusätzliche Daten an AAM zu senden. Darf nicht leer sein und die Größe &lt;= 1024. |

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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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
