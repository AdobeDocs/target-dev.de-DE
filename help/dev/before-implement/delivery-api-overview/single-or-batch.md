---
title: Adobe Target-Bereitstellungs-API - Einzelversand oder Batch-Bereitstellung
description: Verwendung [!UICONTROL Adobe Target-Bereitstellungs-API] Einzelne oder Batch-Bereitstellungsaufrufe?
keywords: Versandschnittstelle
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Einzelversand oder Batch-Bereitstellung

Die [!UICONTROL Adobe Target-Bereitstellungs-API] unterstützt einen einzelnen oder Batch-Bereitstellungsaufruf. Es kann eine Server-Anfrage für Inhalte für einzelne oder mehrere Mboxes gestellt werden.

Berücksichtigen Sie die Leistungskosten bei der Entscheidung, einen einzelnen Aufruf vorzunehmen, im Vergleich zu einem Batch-Aufruf. Wenn Sie alle Inhalte kennen, die für einen Benutzer angezeigt werden müssen, empfiehlt es sich, Inhalte für alle Mboxes mit einem einzelnen Batch-Bereitstellungsaufruf abzurufen, um zu vermeiden, dass mehrere einzelne Bereitstellungsaufrufe durchgeführt werden.

## Einzelversand-Aufruf

Sie können ein Erlebnis abrufen, das dem Benutzer für eine Mbox über die [!UICONTROL Adobe Target-Bereitstellungs-API]. Beachten Sie, dass Sie bei einem einzelnen Bereitstellungsaufruf einen weiteren Server-Aufruf starten müssen, um zusätzliche Inhalte für eine Mbox für einen Benutzer abzurufen. Dies kann im Laufe der Zeit sehr kostspielig werden. Beurteilen Sie daher Ihren Ansatz bei der Verwendung des einzelnen Versand-API-Aufrufs.

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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

Im Beispiel für einen einzelnen Versand-Aufruf oben wird das Erlebnis abgerufen, das dem Benutzer mit `tntId`: `abcdefghijkl00023.1_1` für `mbox`:`SummerOffer` im Webkanal. Dieser einzelne Bereitstellungsaufruf generiert die folgende Antwort:

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

Beachten Sie in der Antwort die `content` -Feld enthält die HTML, die das Erlebnis beschreibt, das dem Benutzer für das Web angezeigt werden soll, das der Mbox SummerOffer entspricht.

### Ausführen des Seitenladevorgangs

Wenn es Erlebnisse gibt, die angezeigt werden sollen, wenn eine Seite im Webkanal geladen wird, z. B. A-Tests für die Schriftarten in der Fußzeile oder Kopfzeile, können Sie Folgendes festlegen: `pageLoad` im `execute` -Feld, um alle Änderungen abzurufen, die angewendet werden sollen.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
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
  "execute": {
    "pageLoad": {}
  }
}'
```

Der obige Beispielaufruf ruft alle Erlebnisse ab, um einen Benutzer bei der Seite anzuzeigen `https://target.enablementadobe.com/react/demo/#/` lädt.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

Im `content` -Feld die Änderung, die beim Laden einer Seite angewendet werden muss, kann abgerufen werden. Im obigen Beispiel muss ein Link in der Kopfzeile benannt werden. *Geänderte Startseite*.

## Batch-Bereitstellungsaufruf

Anstatt mehrere Bereitstellungsaufrufe mit einer einzelnen Mbox in jedem Aufruf durchzuführen, kann ein Bereitstellungsaufruf mit einem Batch von Mboxes unnötige Server-Aufrufe reduzieren. Das Aufrufen eines Server-Aufrufs sollte so weit wie möglich minimiert werden, um eine hohe Leistung zu erzielen.

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
    "execute": {
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

Im obigen Beispiel für einen Batch-Bereitstellungsaufruf werden Erlebnisse abgerufen, die für den Benutzer mit `tntId`: `abcdefghijkl00023.1_1` für mehrere `mbox`:`SummerOffer`, `SummerShoesOffer`, und `SummerDressOffer`. Da wir wissen, dass wir für diesen Benutzer ein Erlebnis für mehrere Mboxes anzeigen müssen, können wir diese Anfragen in einem Batch-Vorgang speichern und einen Server-Aufruf anstelle von drei individuellen Bereitstellungsaufrufen durchführen.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
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

In der obigen Antwort sehen Sie dies in der `content` -Feld jeder Mbox, kann die HTML-Darstellung des Erlebnisses abgerufen werden, das dem Benutzer für jede Mbox angezeigt wird.
