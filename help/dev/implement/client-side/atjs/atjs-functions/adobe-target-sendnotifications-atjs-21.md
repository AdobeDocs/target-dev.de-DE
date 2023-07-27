---
keywords: adobe.target.sendNotifications, sendNotifications, sendnotifications, send notifications, sending notifications, notifications, at.js, Funktionen, funktion, $9
description: Verwendung [!UICONTROL adobe.target.sendNotifications()] für at.js zum Senden von Benachrichtigungen an die [!DNL Target] Edge, wenn ein Erlebnis nicht mit [!UICONTROL applyOffer]s). (at.js.2.1 +)
title: Wie verwende ich die Funktion adobe.target.sendNotifications()?
feature: at.js
exl-id: 1a08da10-31a0-4b0b-af7d-91ed7d32c308
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 84%

---

# [!UICONTROL adobe.target.sendNotifications(options)]

Diese Funktion sendet eine Benachrichtigung an [!DNL Target] Edge, wenn ein Erlebnis ohne Verwendung von `[!UICONTROL adobe.target.applyOffer()]` oder `[!UICONTROL adobe.target.applyOffers()]`.

>[!NOTE]
>
>Diese Funktion wurde in at.js 2.1.0 eingeführt und steht für Versionen höher als 2.1.0 zur Verfügung.

| Schlüssel | Typ | Erforderlich? | Beschreibung |
| --- | --- | --- | --- |
| consumerId | Zeichenfolge | Nein | Der Standardwert ist die globale Mbox des Kunden, falls nicht angegeben. Dieser Schlüssel wird verwendet, um die ID für zusätzliche Daten zu generieren, die für die A4T-Integration verwendet wird. |
| Anfrage | Objekt | Ja | Siehe Anforderungstabelle unten. |
| Zeitüberschreitung | Nummer | Nein | Zeitüberschreitung der Abfrage. Wenn nicht angegeben, wird die standardmäßige at.js-Zeitüberschreitung verwendet. |

## Anfrage

| Feldname | Typ | Erforderlich? | Einschränkung | Beschreibung |
| --- | --- | --- | --- | --- |
| Request > notifications | Array von Objekten | Ja |  | Benachrichtigungen für den angezeigten Inhalt, angeklickte Selektoren und/oder besuchte Ansichten oder Mboxes. |
| Request > notifications > address | Objekt | Nein |  |  |
| Request > notifications > address > url | Zeichenfolge | Nein |  | URL, über die die Benachrichtigung ausgelöst wurde. |
| Request > notifications > address > referringUrl | Zeichenfolge | Nein |  | Die Referenz-URL, über die die Benachrichtigung ausgelöst wurde. |
| Request > notifications > parameters | Zeichenfolge | Nein | Die folgenden Namen sind für Parameter nicht zulässig:<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Beachten Sie Folgendes:<ul><li>Maximale Begrenzung für Parameter: 50.</li><li>Der Parametername darf nicht leer sein.</li><li>Maximale Länge des Parameternamens: 128</li><li>Parameternamen dürfen nicht mit „profile“ beginnen.</li><li>Maximale Wertelänge des Parameters: 5.000.</li></ul> |  |
| Request > notifications > profileParameters | Zeichenfolge | Nein | Die folgenden Namen sind für Parameter nicht zulässig:<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>Beachten Sie Folgendes:<ul><li>Maximale Begrenzung für Parameter: 50.</li><li>Der Parametername darf nicht leer sein.</li><li>Maximale Länge des Parameternamens: 128</li><li>Parameternamen dürfen nicht mit „profile“ beginnen.</li><li>Maximale Wertelänge: 5.000.</li></ul> |  |
| Request > notifications > order | Objekt | Nein |  | Objekt, das die Bestelldetails beschreibt. |
| Request > notifications > order > id | Zeichenfolge | Nein | `<=` 250 Zeichen. | Bestell-ID. |
| Request > notifications > order > total | Zeichenfolge | Nein | `>=` 0 | Bestellsumme. |
| Request > notifications > order > purchasedProductIds | Zeichenfolgen-Array | Nein | <ul><li>Keine leeren Werte zulässig.</li><li>Maximale Länger der Produkt-ID: 50</li><li>Produkt-IDs (durch Kommas getrennt und verkettet) dürfen eine Gesamtlänge von 250 nicht überschreiten.</li></ul> | Bestellprodukt-IDs. |
| Request > notifications > product | Objekt | Nein |  |  |
| Request > notifications > product > id | Zeichenfolge | Nein | `<=` 128 Zeichen; darf nicht leer sein. | Produkt-ID. |
| Request > notifications > product > categoryId | Zeichenfolge | Nein | `<=` 128 Zeichen; darf nicht leer sein. | Kategorie-ID. |
| Request > notifications > id | Zeichenfolge | Ja | `<=` 200 Zeichen. | Die Benachrichtigungs-ID wird in der Antwort zurückgegeben und gibt an, dass die Benachrichtigung erfolgreich verarbeitet wurde. |
| Request > notifications > impressionId | Zeichenfolge | Nein | `<= 128` Zeichen. | Die Impressions-ID wird verwendet, um die aktuelle Benachrichtigung mit einer vorherigen Benachrichtigung oder Ausführungsanforderung zu verknüpfen. Stimmen beide überein, generieren die zweite sowie andere nachfolgende Anforderungen keine neue Impression für die Aktivität oder das Erlebnis. |
| Anforderung > Benachrichtigungen > Typ | Zeichenfolge | Ja | &quot;click&quot;oder &quot;display&quot;wird unterstützt. | Benachrichtigungstyp. |
| Request > notifications > timestamp | Nummer`<int64>` | Ja |  | Zeitstempel der Benachrichtigung in Millisekunden, die seit Beginn der UNIX-Epoche verstrichen sind. |
| Request > notifications > tokens | Zeichenfolgen-Array | Ja |  | Eine Liste der Token für angezeigte Inhalte oder angeklickte Selektoren basierend auf dem Typ der Benachrichtigung. |
| Request > notifications > mbox | Objekt | Nein |  | Benachrichtigungen für die Mbox. |
| Request > notifications > mbox > name | Zeichenfolge | Nein | Keine leeren Werte zulässig.<p>Zulässige Zeichen: Siehe Hinweis nach dieser Tabelle. | Name der Mbox. |
| Request > notifications > mbox > state | Zeichenfolge | Nein |  | Mbox-Statustoken. |
| Request > notifications > view | Objekt | Nein |  |  |
| Request > notifications > view > id | Ganzzahl `<int64>` | Nein |  | Ansicht-ID Die ID, die der Ansicht zugewiesen wurde, als die Ansicht über die Ansicht-API erstellt wurde. |
| Request > notifications > view > name | Zeichenfolge | Nein | `<= 128` Zeichen | Name der Ansicht. |
| Request > notifications > view > key | Zeichenfolge | Nein | `<=` 512 Zeichen. | Ansichtsschlüssel. Der Schlüssel, der mit der Ansicht über die API festgelegt wurde. |
| Request > notifications > view > state | Zeichenfolge | Nein |  | Token für den Ansichtsstatus. |

**Hinweis**: Die folgenden Zeichen sind *not* zulässig für `Request > notifications > mbox > name`:

```
- '-, ./=`:;&!@#$%^&*()+|?~[]{}'
```

## sendNotifications()-Aufruf nach dem Rendern vorgeladener Mboxes

```javascript {line-numbers="true"}
function createTokens(options) {
  return options.map(e => e.eventToken);
}

function createNotification(mbox, type, tokens) {
  const id = 11111; // here we should use a random ID like UUID
  const timestamp = Date.now();
  const { name, state, parameters, profileParameters, order, product } = mbox;
  const result = {
    id,
    type,
    timestamp,
    parameters,
    profileParameters,
    order,
    product
  };

  result.mbox = { name, state };
  result.tokens = tokens;

  return result;
}

adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "a1-serverside-ab"
        }
      ]
    }
  }
})
.then(response => {
  const mboxes = response.prefetch.mboxes;
  const notifications = mboxes.map(mbox => {
    const type = "display";
    const tokens = createTokens(mbox.options);

    return createNotification(mbox, type, tokens);
  });
  
  adobe.target.sendNotifications({
    request: { notifications }
  });
})
```

>[!NOTE]
>
>Wenn Sie [!DNL Adobe Analytics], `[!UICONTROL getOffers()]` nur mit Vorabruf und `[!UICONTROL sendNotifications()]`, die [!DNL Analytics] -Anforderung ausgelöst werden, nachdem `[!UICONTROL sendNotifications()]` ausgeführt wird. Dadurch soll sichergestellt werden, dass die durch `[!UICONTROL sendNotifications()]` entspricht der SDID, die an gesendet wird [!DNL Analytics] und [!DNL Target].
