---
keywords: adobe.target.getOffers, getOffers, getOffers, getOffers, at.js, Funktionen, Funktion, $8
description: Verwenden Sie die [!UICONTROL adobe.target.getOffers()]-Funktion und ihre Optionen für die  [!DNL Adobe Target] .js-Bibliothek, um Anfragen auszulösen, um mehrere  [!DNL Target]  zu erhalten. (at.js 2.x)
title: Wie verwende ich die [!UICONTROL adobe.target.getOffers()]?
feature: at.js
exl-id: b96a3018-93eb-49e7-9aed-b27bd9ae073a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 62%

---

# [!UICONTROL adobe.target.getOffers()] - at.js 2.x

Mit dieser Funktion können Sie mehrere Angebote abrufen, indem Sie mehrere Mboxes übergeben. Darüber hinaus können mehrere Angebote für alle Ansichten in aktiven Aktivitäten abgerufen werden.

>[!NOTE]
>
>Diese Funktion wurde mit at.js 2.x eingeführt. Diese Funktion steht für at.js Version 1 nicht zur Verfügung.*x*.

| Schlüssel | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| `consumerId` | Zeichenfolge | Nein | Der Standardwert ist die globale Mbox des Kunden, falls nicht angegeben. Dieser Schlüssel wird verwendet, um die zusätzliche Daten-ID (SDID) zu generieren, die für die A4T-Integration verwendet wird.<P>Bei Verwendung von `getOffers()` generiert jeder Aufruf eine neue SDID. Wenn Sie mehrere Mbox-Anfragen auf derselben Seite haben und die SDID beibehalten möchten (sodass sie mit der SDID aus der target-global-mbox und der [!DNL Adobe Analytics] SDID übereinstimmt), verwenden Sie den `consumerId`.<P>Wenn `getOffers()` drei Mboxes enthält (mit den Namen „mbox1“, „mbox2“ und „mbox3„), schließen Sie Folgendes ein: `consumerId: "mbox1, mbox2, mbox3"` in den `getOffers()` Aufruf. |
| `decisioningMethod` | Zeichenfolge | Nein | „Server-seitig“, „On-Device“, „Hybrid“ |
| `request` | Objekt | Ja | Siehe Anforderungstabelle unten. |
| `timeout` | Nummer | Nein | Zeitüberschreitung der Abfrage. Wenn nicht angegeben, wird die standardmäßige at.js-Zeitüberschreitung verwendet. |

## Anfrage

>[!NOTE]
>
>In der [Dokumentation zur Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) finden Sie Informationen zu den akzeptablen Typen für alle unten aufgeführten Felder.

| Feldname | Erforderlich? | Einschränkungen | Beschreibung |
| --- | --- | --- | --- |
| Anfrage > ID | Nein |  | Entweder `tntId`, `thirdPartyId` oder `marketingCloudVisitorId` wird benötigt. |
| Anfrage > ID > thirdPartyId | Nein | Maximale Größe = 128. |  |  |
| Request > experienceCloud | Nein |  |  |
| Request > experienceCloud > analytics | Nein |  | Adobe Analytics-Integration |
| Request > experienceCloud > analytics > logging | Nein | Folgendes muss auf der Seite implementiert werden:<ul><li>Besucher-ID-Service</li><li>Appmeasurement.js</li></ul> | Die folgenden Werte werden unterstützt:<P>**client_side**: Wenn angegeben, wird eine Analytics-Payload an den Aufrufer zurückgegeben, die zum Senden an [!UICONTROL Adobe Analytics] über die [!UICONTROL Data Insertion API] verwendet werden sollte.<P>**server_side**: Dies ist der Standardwert, bei dem der [!DNL Target] und [!DNL Analytics] Backend die SDID verwenden, um die Aufrufe zu Berichtszwecken zusammenzufügen. |
| Anfrage > Vorab abrufen | Nein |  |  |
| Anfrage > Vorab abrufen > Ansichten | Nein | Maximale Anzahl 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Wertelänge `<=` 5000.<P>Der Name darf nicht mit „profile“ beginnen.<P>Nicht zulässige Namen: „orderId“, „orderTotal“, „productPurchasedId“. | Parameter übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > profileParameters | Nein | Maximale Anzahl 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Wertelänge `<=` 5000.<P>Akzeptiert nur Zeichenfolgenwerte.<P>Der Name darf nicht mit „profile“ beginnen. | Profilparameter übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > Produkt | Nein |  |  |
| Anfrage > Vorab abrufen > Ansichten > Produkt -> ID | Nein | Nicht leer.<P>Maximale Größe = 128. | Produkt-IDs übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > Produkt > categoryId | Nein | Nicht leer.<P>Maximale Größe = 128. | Produktkategorie-IDs übergeben, die zum Aufrufen relevanter Ansichten in Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > Bestellung | Nein |  |  |
| Anfrage > Vorab abrufen > Ansichten > Bestellung > ID | Nein | Maximale Länge = 250. | Bestell-IDs übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > Bestellung > Gesamtsumme | Nein | Insgesamt `>=` 0. | Gesamtbestellsummen übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Vorab abrufen > Ansichten > Bestellung > purchasedProductIds | Nein | Keine leeren Werte.<P>Die maximale Länge jedes Werts ist 50.<P>Verkettet und durch Kommas getrennt.<P>Die Gesamtlänge der Produkt-IDs `<=` 250. | IDs gekaufter Produkte übergeben, die zum Aufrufen relevanter Ansichten in aktiven Aktivitäten verwendet werden können. |
| Anfrage > Ausführen | Nein |  |  |
| Anfrage > Ausführen > pageLoad | Nein |  |  |
| Anfrage > Ausführen > pageLoad > Parameter | Nein | Maximale Anzahl 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Wertelänge `<=` 5000.<P>Akzeptiert nur Zeichenfolgenwerte.<P>Der Name darf nicht mit „profile“ beginnen.<P>Nicht zulässige Namen: „orderId“, „orderTotal“, „productPurchasedId“. | Angebote mit angegeben Parametern abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > profileParameters | Nein | Maximale Anzahl 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Länge des Werts `<=`256.<P>Der Name darf nicht mit „profile“ beginnen.<P>Akzeptiert nur Zeichenfolgenwerte. | Angebote mit angegeben Profilparametern abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > Produkt | Nein |  |  |
| Anfrage > Ausführen > pageLoad > Produkt -> ID | Nein | Nicht leer.<P>Maximale Größe = 128. | Angebote mit angegebenen Parametern abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > Produkt > categoryId | Nein | Nicht leer.<P>Maximale Größe = 128. | Angebote mit angegebenen Produktkategorie-IDs abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > Bestellung | Nein |  |  |
| Anfrage > Ausführen > pageLoad > Bestellung > ID | Nein | Maximale Länge = 250. | Angebote mit angegebenen Bestell-IDs abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > Bestellung > Gesamtsumme | Nein | `>=` 0. | Angebote mit angegebenen Gesamtbestellsummen abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > pageLoad > Bestellung > purchasedProductIds | Nein | Keine leeren Werte.<P>Die maximale Länge jedes Werts ist 50.<P>Verkettet und durch Kommas getrennt.<P>Die Gesamtlänge der Produkt-IDs `<=` 250. | Angebote mit angegebenen IDs gekaufter Produkte abrufen, wenn die Seite geladen wird. |
| Anfrage > Ausführen > Mboxes | Nein | Maximale Größe = 50.<P>Keine Null-Elemente. |  |
| Anfrage > Ausführen > Mboxes > Mbox | Ja | Nicht leer.<P>Kein &quot;-geklickt“-Suffix.<P>Maximale Größe = 250.<P>Zulässige Zeichen: `'-, ._\/=:;&!@#$%^&*()_+|?~[]{}'` | Name der Mbox. |
| Anfrage > Ausführen > Mboxes > Mbox > Index | Ja | Nicht null.<P>Eindeutig.<P>`>=` 0. | Beachten Sie, dass der Index nicht die Reihenfolge darstellt, in der die Mboxes verarbeitet werden. Wie auf einer Webseite mit mehreren regionalen Mboxes kann die Reihenfolge, in der sie verarbeitet werden, nicht angegeben werden. |
| Anfrage > Ausführen > Mboxes > Mbox > Parameter | Nein | Maximale Anzahl = 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Akzeptiert nur Zeichenfolgenwerte.<P>Wertelänge `<=` 5000.<P>Der Name darf nicht mit „profile“ beginnen.<P>Nicht zulässige Namen: „orderId“, „orderTotal“, „productPurchasedId“. | Angebote für eine bestimmte Mbox mit den angegebenen Parametern abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > profileParameters | Nein | Maximale Anzahl = 50.<P>Name nicht leer.<P>Namenslänge `<=` 128.<P>Akzeptiert nur Zeichenfolgenwerte.<P>Länge des Werts `<=`256.<P>Der Name darf nicht mit „profile“ beginnen. | Angebote für eine bestimmte Mbox mit den angegebenen Profilparametern abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > Produkt | Nein |  |  |
| Anfrage > Ausführen > Mboxes > Mbox > Produkt > ID | Nein | Nicht leer.<P>Maximale Größe = 128. | Angebote für eine bestimmte Mbox mit den angegebenen Produkt-IDs abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > Produkt > categoryId | Nein | Nicht leer.<P>Maximale Größe = 128. | Angebote für eine bestimmte Mbox mit den angegebenen Produktkategorie-IDs abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > Bestellung | Nein |  |  |
| Anfrage > Ausführen > Mboxes > Mbox > Bestellung > ID | Nein | Maximale Länge = 250. | Angebote für eine bestimmte Mbox mit den angegebenen Bestell-IDs abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > Bestellung > Gesamtsumme | Nein | `>=` 0. | Angebote für eine bestimmte Mbox mit den angegebenen Gesamtbestellsummen abrufen. |
| Anfrage > Ausführen > Mboxes > Mbox > Bestellung > purchasedProductIds | Nein | Keine leeren Werte.<P>Maximale Länge jedes Werts = 50.<P>Verkettet und durch Kommas getrennt.<P>Produkt-IDs `<=` 250. | Angebote für eine bestimmte Mbox mit den angegebenen IDs der gekauften Produkte der Bestellung abrufen. |

## Benutzen Sie [!UICONTROL getOffers()], um alle Ansichten aufzurufen

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
      prefetch: {
        views: [{}]
    }
  }
});
```

## [!UICONTROL getOffers()] aufrufen, um eine geräteinterne Entscheidung zu treffen

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
}); 
```

## Benutzen Sie [!UICONTROL getOffers()], um die neuesten Ansichten mit den übergebenen Parametern und Profilparametern aufzurufen

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    "prefetch": {
      "views": [
        {
          "parameters": {
            "ad": "1"
          },
          "profileParameters": {
            "age": 23
          }
        }
      ]
    }
  }
});
```

## Benutzen Sie [!UICONTROL getOffers()], um Mboxes mit den übergebenen Parametern und Profilparametern aufzurufen

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    execute: {
      mboxes: [
        {
          index: 0,
          name: "first-mbox"
        },
        {
          index: 1,
          name: "second-mbox",
          parameters: {
            a: 1
          },
          profileParameters: {
            b: 2
          }
        }
      ]
    }
  }
});
```

## Rufen Sie [!UICONTROL getOffers()] auf, um die Analyse-Payload von der Client-Seite abzurufen

```javascript {line-numbers="true"}
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

**Antwort**:

```javascript {line-numbers="true"}
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Die Payload kann dann über die „Data Insertion [&quot; an [!DNL Adobe Analytics] weitergeleitet ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

## Abrufen und Rendern von Daten aus mehreren Mboxes über [!UICONTROL getOffers()] und [!UICONTROL applyOffers()]

Mit at.js 2.x können Sie mehrere Mboxes über die `[!UICONTROL getOffers()]`-API abrufen. Sie können auch Daten für mehrere Mboxes abrufen und dann `[!UICONTROL applyOffers()]` zum Rendern der Daten an verschiedenen Positionen verwenden, die durch einen CSS-Selektor identifiziert werden.

Das folgende Beispiel zeigt eine einfache HTML-Seite, auf der at.js 2.x implementiert ist:

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>at.js 2.x, multiple selectors and multiple mboxes</title>
  <script src="at.js"></script>
</head>
<body>
  <div id="container1">Default content 1</div>
  
  <div id="container2">Default content 2</div>

  <div id="container3">Default content 3</div>
</body>
</html>
```

Angenommen, Sie haben drei Behälter, die Sie über einen Inhalt ändern möchten, der von [!DNL Target] empfangen wurde. Sie können eine einzelne Anfrage für drei Mboxes erstellen, in der jede Mbox Inhalt in den entsprechenden Behälter rendert.

Die Anfrage und der Rendercode könnten wie folgt aussehen:

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "mbox1"
        },
        {
          index: 1,
          name: "mbox2"
        },
        {
          index: 2,
          name: "mbox3"
        }
      ]
    }
  }
})
.then(response => {
  // get all mboxes from response
  const mboxes = response.prefetch.mboxes;
  let count = 1;

  mboxes.forEach(el => {
    adobe.target.applyOffers({
      selector: "#container" + count,
      response: {
        prefetch: {
          mboxes: [el]
        }
      }
    });

    count += 1;
  });
});
```

Im Abschnitt `request > prefetch > mboxes` gibt es drei verschiedene Mboxes. Wenn die Anfrage erfolgreich abgeschlossen wurde, erhalten Sie die Antwort für jede Mbox aus `response > prefetch > mboxes`. Nachdem Sie über die Antworten und die Speicherorte für die Wiedergabe verfügen, können Sie `applyOffers()` aufrufen, um den von Ihnen von [!DNL Target] abgerufenen Inhalt wiederzugeben. In diesem Beispiel haben wir die folgende Zuordnung:

* Mbox 1 > CSS selector # container 1
* Mbox 2 > CSS selector # container 2
* Mbox 3 > CSS selector # container 3

In diesem Beispiel werden die CSS-Selektoren mit einer Zähl-Variablen erstellt. In einem realen Szenario könnten Sie zwischen dem CSS-Selektor und der Mbox eine andere Zuordnung verwenden.

Beachten Sie, dass dieses Beispiel `prefetch > mboxes` verwendet, Sie könnten aber auch `execute > mboxes` verwenden. Stellen Sie sicher, dass Sie bei Verwendung von Vorausholen (prefetch) in `getOffers()` auch beim Aufruf von `applyOffers()` Vorausholen verwenden sollten.

## Aufrufen von [!UICONTROL getOffers()] zum Ausführen eines Seitenladevorgangs

Das folgende Beispiel zeigt, wie Sie einen pageLoad mit [!UICONTROL getOffers()] mit at.js 2 durchführen.*x*  

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {
                parameters: {}
            }
        }
    }
});
```
