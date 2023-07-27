---
title: Ausführen von Funktionstests mit Attributen
description: Ausführen von Funktionstests mit Attributen
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Ausführen von Funktionstests mit Attributen

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation
1. Erstellen Sie eine [!UICONTROL A/B-Test] activity
1. A und B definieren
1. Hinzufügen einer Zielgruppe
1. Traffic-Zuordnung festlegen
1. Traffic-Verteilung auf Varianten festlegen
1. Berichterstellung einrichten
1. Metriken zur Verfolgung von KPIs hinzufügen
1. Implementieren von Code zum Ausführen von Funktionstests mit Attributen
1. Implementieren von Code zur Verfolgung von Konversionsereignissen
1. Aktivieren Ihrer Funktionstests mit Attributen

>[!NOTE]
>
>Angenommen, Sie sind ein E-Commerce-Einzelhandelsunternehmen. Sie möchten die Konversionsrate erhöhen, wenn Kunden Ihren Produktkatalog durchsuchen und sortieren. Sie haben die Hypothese, dass bestimmte Sortierungsalgorithmen und Paginierungsstrategien bessere Ergebnisse liefern als andere. Um diese Theorie zu testen, führen Sie einen Funktionstest durch, bei dem das Sortierungs-Widget mit verschiedenen Sortierungsoptionen für Ihre Endbenutzer neu gestaltet wird. Sie möchten sicherstellen, dass dieser Funktionstest bei nahezu null Latenz ausgeführt wird, sodass er keine negativen Auswirkungen auf Benutzererlebnisse hat und die Ergebnisse verfälscht.

## 1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** in [!DNL Adobe Target]und aktivieren Sie die **[!UICONTROL On-Device Decisioning]** umschalten.

![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über einen Administrator oder Genehmiger verfügen. [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um die **[!UICONTROL On-Device Decisioning]** umschalten.

Nach der Aktivierung der **[!UICONTROL On-Device Decisioning]** Umschalten, [!DNL Adobe Target] beginnt zu generieren *ruleArtefakte* für Ihren Client.

## 2. Erstellen Sie eine [!UICONTROL A/B-Test] activity

1. In [!DNL Adobe Target], navigieren Sie zum **[!UICONTROL Tätigkeiten]** Seite und wählen Sie **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

   ![ALT-Bild](assets/asset-ab.png)

1. Im **[!UICONTROL A/B-Test-Aktivität erstellen]** modal, Behalten Sie die Standardeinstellung bei **[!UICONTROL Web]** ausgewählte Option (1), wählen Sie **[!UICONTROL Formular]** Wählen Sie als Experience Composer (2) **[!UICONTROL Standardarbeitsbereich]** mit **[!UICONTROL Keine Eigenschaftenbeschränkungen]** (3) und klicken Sie auf **[!UICONTROL Nächste]** 4.

   ![ALT-Bild](assets/asset-form.png)

## 3. Definieren Sie Ihre A und B

1. Im **[!UICONTROL Erlebnisse]** Schritt der Aktivitätserstellung einen Namen für Ihre Aktivität angeben (1) und ein zweites Erlebnis, Erlebnis B, hinzufügen, indem Sie auf die **[!UICONTROL Erlebnis hinzufügen]** (2). Geben Sie den Namen des Speicherorts (3) in Ihrer Anwendung ein, an dem Sie Ihren Funktionstest mit Attributen ausführen möchten. Im folgenden Beispiel: `product-results-page` der für Erlebnis A definierte Ort (er ist auch der für Erlebnis B definierte Ort)

   ![ALT-Bild](assets/asset-location.png)

   **[!UICONTROL Erlebnis A]** enthält die JSON-Datei, die Ihre Geschäftslogik für Folgendes signalisiert:

   * Initiieren der Sortierungsalgorithmus-Funktion über die `test_sorting` Feature Flag
   * Führen Sie den empfohlenen Sortieralgorithmus aus, der im `sorting_algorithm _**_attribute`
   * Gibt 50 Produkte pro Seite zurück, wie durch die in der Variablen `pagination_limit`

1. Klicken Sie in Erlebnis A auf , um den Inhalt von **[!UICONTROL Standardinhalt]** durch Auswahl von **[!UICONTROL JSON-Angebot erstellen]** wie unten gezeigt (1).

   ![ALT-Bild](assets/asset-offer.png)

1. Definieren Sie die JSON mit `test_sorting`, `sorting_algorithm`, und `pagination_limit` Flags und Attribute, mit denen der empfohlene Sortieralgorithmus mit einer Paginierungsgrenze von 50 Produkten initiiert wird.

   >[!NOTE]
   >
   >Wann [!DNL Adobe Target] erfasst einen Benutzer, um Erlebnis A anzuzeigen, wird die JSON mit den definierten Attributen im Beispiel zurückgegeben. In Ihrem Code müssen Sie den Wert des Feature Flag überprüfen `test_sorting` , um zu sehen, ob die Sortierfunktion aktiviert werden soll. Wenn ja, verwenden Sie den empfohlenen Wert der `sorting_algorithm` -Attribut, um die empfohlenen Produkte in der Produktlistenansicht anzuzeigen. Die Produktbegrenzung, die für Ihre Anwendung angezeigt werden soll, beträgt 50, da dies der Wert der Variablen `pagination_limit` -Attribut.

   ![ALT-Bild](assets/asset-sorting.png)

   **[!UICONTROL Erlebnis B]** definiert die JSON-Datei, die Ihre Geschäftslogik für Folgendes signalisiert:

   * Initiieren der Sortierungsalgorithmus-Funktion über das Feature Flag test_sort
   * Führen Sie die `best_sellers` Sortieralgorithmus, der im `sorting_algorithm _**_attribute`
   * Gibt 50 Produkte pro Seite zurück, wie durch die in der Variablen `pagination_limit`

   >[!NOTE]
   >
   >Wann [!DNL Adobe Target] einen Benutzer erfasst, um Erlebnis B anzuzeigen, wird die JSON mit den definierten Attributen im Beispiel zurückgegeben. In Ihrem Code müssen Sie den Wert des Feature Flag überprüfen `test_sorting` , um zu sehen, ob die Sortierfunktion aktiviert werden soll. Wenn ja, verwenden Sie die `best_sellers` Wert der `sorting_algorithm` -Attribut verwenden, um Produkte mit dem besten Verkauf in der Produktlistenansicht anzuzeigen. Die Produktbegrenzung, die für Ihre Anwendung angezeigt werden soll, beträgt 50, da dies der Wert der Variablen `pagination_limit` -Attribut.

   ![ALT-Bild](assets/asset-sorting-b.png)

## 4. Audience hinzufügen

Im **[!UICONTROL Targeting]** halten Sie die **[!UICONTROL Alle Besucher]** Zielgruppe. Auf diese Weise können Sie die Auswirkungen Ihrer Sortierfunktion sowie den am besten beeinflussenden Algorithmus und die Anzahl der Elemente nachvollziehen.

![ALT-Bild](assets/asset-audience-b.png)

## 5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz Ihrer Besucher, mit dem Sie Ihre Sortieralgorithmen und Paginierungsstrategie testen möchten. Mit anderen Worten, zu welchem Prozentsatz Ihrer Benutzer möchten Sie diesen Test einführen? Um diesen Test für alle angemeldeten Benutzer bereitzustellen, halten Sie die Traffic-Zuordnung in diesem Beispiel bei 100 %.

![ALT-Bild](assets/asset-allocation-100.png)

## 6. Traffic-Verteilung auf Varianten festlegen

Definieren Sie den Prozentsatz Ihrer Besucher, denen der empfohlene Algorithmus zur Sortierung der besten Verkäufer angezeigt wird, mit einer Beschränkung von 50 Produkten pro Seite. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![ALT-Bild](assets/asset-variations-50.png)

## 7. Einrichten von Berichten

Im **[!UICONTROL Ziele und Einstellungen]** Schritt auswählen **[!UICONTROL Adobe Target]** als **[!UICONTROL Berichtsquelle]** um Ihre A/B-Testergebnisse im [!DNL Adobe Target] Benutzeroberfläche oder wählen Sie **[!UICONTROL Adobe Analytics]** , um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![ALT-Bild](assets/asset-reporting-b.png)

## 8. Hinzufügen von Metriken zur Verfolgung von KPIs

Wählen Sie eine **[!UICONTROL Zielmetrik]** , um den Funktionstest mit Attributen zu messen. In diesem Beispiel basiert der Erfolg darauf, ob der Benutzer ein Produkt kauft, je nach dem angezeigten Sortieralgorithmus und der angezeigten Paginierungsstrategie.

## 9. Implementieren von Funktionstests mit Attributen in Ihre Anwendung

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java ]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10. Implementieren Sie Code zur Verfolgung von Konversionsereignissen

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "product-results-page"
          }
        }
      ]
    }
})
```

>[!TAB Java ]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11. Aktivieren Sie Ihre Funktionstests mit Attributen

![ALT-Bild](assets/asset-activate.png)
