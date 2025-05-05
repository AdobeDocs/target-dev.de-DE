---
title: Adobe Target-Bereitstellungs-API-Benachrichtigungen
description: Wie löse ich Benachrichtigungen mithilfe der [!UICONTROL Adobe Target Delivery API] aus?
keywords: Bereitstellungs-API
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Benachrichtigungen

Benachrichtigungen sollten ausgelöst werden, wenn eine im Voraus abgerufene mbox oder Ansicht besucht oder für den Endbenutzer gerendert wurde.

Damit Benachrichtigungen für die richtige Mbox oder Ansicht ausgelöst werden, müssen Sie für jede Mbox oder Ansicht den Überblick über die entsprechenden `eventToken` behalten. Benachrichtigungen mit den richtigen `eventToken` für die entsprechenden Mboxes oder Ansichten müssen ausgelöst werden, damit Berichte korrekt widergespiegelt werden.

## Benachrichtigungen für im Voraus abgerufene Mboxes

Eine oder mehrere Benachrichtigungen können über einen einzigen Versandaufruf gesendet werden. Ermitteln Sie, ob es sich bei der zu verfolgenden Metrik entweder um eine `click` oder eine `display` für jede Mbox handelt, damit die `type` der Benachrichtigung korrekt dargestellt werden kann. Übergeben Sie außerdem für jede Benachrichtigung eine `id`, damit festgestellt werden kann, ob eine Benachrichtigung korrekt über die gesendet wurde[!UICONTROL &#x200B; Adobe Target Delivery API]. Die `timestamp` ist auch wichtig, an [!DNL Target] weitergeleitet zu werden, um anzugeben, wann die `click` oder `display` für eine bestimmte Mbox zu Berichtszwecken aufgetreten ist.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
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
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

Der obige Beispielaufruf führt zu einer Antwort, die anzeigt, dass die `notifications` erfolgreich verarbeitet wurde.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

Wenn alle an [!DNL Target] gesendeten `notifications` ordnungsgemäß verarbeitet sind, werden sie im `notifications`-Array in der Antwort angezeigt. Wenn jedoch eine `notifications` `id` fehlt, ist diese `notification` nicht durchgegangen. In diesem Szenario kann eine Logik für weitere Zustellversuche eingerichtet werden, bis eine erfolgreiche `notification`-Antwort abgerufen wird. Stellen Sie sicher, dass für die Wiederholungslogik eine Zeitüberschreitung angegeben ist, damit der API-Aufruf nicht blockiert wird und zu Leistungsverzögerungen führt.

## Benachrichtigungen für vorab abgerufene Ansichten

Eine oder mehrere Benachrichtigungen können über einen einzigen Versandaufruf gesendet werden. Ermitteln Sie, ob es sich bei der zu verfolgenden Metrik entweder um eine `click` oder eine `display` für jede Mbox handelt, damit der Typ der Benachrichtigung korrekt dargestellt werden kann. Übergeben Sie außerdem für jede Benachrichtigung einen `id`, damit festgestellt werden kann, ob eine Benachrichtigung korrekt über die [!UICONTROL Adobe Target Delivery API] gesendet wurde. Der Zeitstempel ist auch wichtig, um an [!DNL Target] weitergeleitet zu werden, um anzugeben, wann die `click` oder `display` für eine bestimmte Ansicht zu Berichtszwecken aufgetreten ist.

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
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

Der obige Beispielaufruf führt zu einer Antwort, die anzeigt, dass die `notifications` erfolgreich verarbeitet wurde.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

Wenn alle an [!DNL Target] gesendeten `notifications` ordnungsgemäß verarbeitet sind, werden sie im `notifications`-Array in der Antwort angezeigt. Wenn jedoch eine `notifications` `id` fehlt, wurde diese Benachrichtigung nicht durchgeführt. In diesem Szenario kann eine Logik für weitere Zustellversuche eingerichtet werden, bis eine erfolgreiche Benachrichtigungsantwort abgerufen wird. Stellen Sie sicher, dass für die Wiederholungslogik eine Zeitüberschreitung angegeben ist, damit der API-Aufruf nicht blockiert wird und zu Leistungsverzögerungen führt.
