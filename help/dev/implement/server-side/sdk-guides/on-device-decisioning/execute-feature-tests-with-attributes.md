---
title: Ausführen von Funktionstests mit Attributen
description: Ausführen von Funktionstests mit Attributen
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---

# Ausführen von Funktionstests mit Attributen

## Zusammenfassung der Schritte

1. [!UICONTROL on-device decisioning] für Ihre Organisation aktivieren
1. Erstellen einer [!UICONTROL A/B Test] -Aktivität
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

## 1. Aktivieren Sie [!UICONTROL on-device decisioning] für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie in [!DNL Adobe Target] zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

![alt image](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die Benutzerrolle &quot;Admin&quot;oder &quot;Genehmiger&quot;[Benutzer](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) verfügen, um den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren oder zu deaktivieren.

Nachdem Sie den Umschalter **[!UICONTROL On-Device Decisioning]** aktiviert haben, beginnt [!DNL Adobe Target] mit der Generierung von *Regel-Artefakten* für Ihren Client.

## 2. Erstellen einer [!UICONTROL A/B Test] -Aktivität

1. Navigieren Sie in [!DNL Adobe Target] zur Seite **[!UICONTROL Activities]** und wählen Sie dann **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]** aus.

   ![alt image](assets/asset-ab.png)

1. Behalten Sie im Modal **[!UICONTROL Create A/B Test Activity]** die standardmäßig ausgewählte Option **[!UICONTROL Web]** bei (1), wählen Sie **[!UICONTROL Form]** als Ihren Experience Composer (2), wählen Sie **[!UICONTROL Default Workspace]** mit **[!UICONTROL No Property Restrictions]** (3) und klicken Sie auf **[!UICONTROL Next]** (4).

   ![alt image](assets/asset-form.png)

## 3. Definieren Sie Ihre A und B

1. Geben Sie im Schritt **[!UICONTROL Experiences]** der Aktivitätserstellung einen Namen für Ihre Aktivität (1) ein und fügen Sie ein zweites Erlebnis, Erlebnis B, hinzu, indem Sie auf die Schaltfläche **[!UICONTROL Add Experience]** (2) klicken. Geben Sie den Namen des Speicherorts (3) in Ihrer Anwendung ein, an dem Sie Ihren Funktionstest mit Attributen ausführen möchten. Im folgenden Beispiel ist `product-results-page` der für Erlebnis A definierte Ort (es ist auch der für Erlebnis B definierte Ort).

   ![alt image](assets/asset-location.png)

   **[!UICONTROL Experience A]** enthält die JSON-Datei, die Ihre Geschäftslogik für Folgendes signalisiert:

   * Initiieren der Sortierungsalgorithmus-Funktion über das Feature Flag `test_sorting`
   * Führen Sie den empfohlenen Sortieralgorithmus aus, der im `sorting_algorithm _**_attribute` definiert ist.
   * Gibt 50 Produkte pro Seite zurück, wie durch die Paginierungsstrategie definiert, die in `pagination_limit` definiert ist.

1. Klicken Sie in Erlebnis A auf , um den Inhalt von **[!UICONTROL Default Content]** in die JSON zu ändern, indem Sie **[!UICONTROL Create JSON Offer]** wie unten gezeigt (1) auswählen.

   ![alt image](assets/asset-offer.png)

1. Definieren Sie die JSON-Datei mit den Flags und Attributen `test_sorting`, `sorting_algorithm` und `pagination_limit`, die verwendet werden, um den empfohlenen Sortieralgorithmus mit einer Paginierungsgrenze von 50 Produkten zu initiieren.

   >[!NOTE]
   >
   >Wenn [!DNL Adobe Target] einen Benutzer erfasst, um Erlebnis A anzuzeigen, wird die JSON mit den definierten Attributen im Beispiel zurückgegeben. In Ihrem Code müssen Sie den Wert des Feature Flag `test_sorting` überprüfen, um zu sehen, ob die Sortierfunktion aktiviert werden soll. Wenn dies der Fall ist, verwenden Sie den empfohlenen Wert des Attributs `sorting_algorithm` , um empfohlene Produkte in der Produktlistenansicht anzuzeigen. Die Anzahl der Produkte, die für Ihre Anwendung angezeigt werden sollen, beträgt 50, da dies der Wert des Attributs `pagination_limit` ist.

   ![alt image](assets/asset-sorting.png)

   **[!UICONTROL Experience B]** definiert die JSON, die Ihre Geschäftslogik für Folgendes signalisiert:

   * Initiieren der Sortierungsalgorithmus-Funktion über das Feature Flag test_sort
   * Führen Sie den im `sorting_algorithm _**_attribute` definierten Sortierungsalgorithmus `best_sellers` aus.
   * Gibt 50 Produkte pro Seite zurück, wie durch die Paginierungsstrategie definiert, die in `pagination_limit` definiert ist.

   >[!NOTE]
   >
   >Wenn [!DNL Adobe Target] einen Benutzer erfasst, um Erlebnis B anzuzeigen, wird die JSON mit den definierten Attributen im Beispiel zurückgegeben. In Ihrem Code müssen Sie den Wert des Feature Flag `test_sorting` überprüfen, um zu sehen, ob die Sortierfunktion aktiviert werden soll. Wenn dies der Fall ist, verwenden Sie den Wert `best_sellers` des Attributs `sorting_algorithm`, um die am besten verkauften Produkte in der Produktlistenansicht anzuzeigen. Die Anzahl der Produkte, die für Ihre Anwendung angezeigt werden sollen, beträgt 50, da dies der Wert des Attributs `pagination_limit` ist.

   ![alt image](assets/asset-sorting-b.png)

## 4. Audience hinzufügen

Behalten Sie im Schritt **[!UICONTROL Targeting]** die Zielgruppe **[!UICONTROL All Visitors]** bei. Auf diese Weise können Sie die Auswirkungen Ihrer Sortierfunktion sowie den am besten beeinflussenden Algorithmus und die Anzahl der Elemente nachvollziehen.

![alt image](assets/asset-audience-b.png)

## 5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz Ihrer Besucher, mit dem Sie Ihre Sortieralgorithmen und Paginierungsstrategie testen möchten. Mit anderen Worten, zu welchem Prozentsatz Ihrer Benutzer möchten Sie diesen Test einführen? Um diesen Test für alle angemeldeten Benutzer bereitzustellen, halten Sie die Traffic-Zuordnung in diesem Beispiel bei 100 %.

![alt image](assets/asset-allocation-100.png)

## 6. Traffic-Verteilung auf Varianten festlegen

Definieren Sie den Prozentsatz Ihrer Besucher, denen der empfohlene Algorithmus zur Sortierung der besten Verkäufer angezeigt wird, mit einer Beschränkung von 50 Produkten pro Seite. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![alt image](assets/asset-variations-50.png)

## 7. Einrichten von Berichten

Wählen Sie im Schritt **[!UICONTROL Goals & Settings]** die Option **[!UICONTROL Adobe Target]** als **[!UICONTROL Reporting Source]**, um Ihre A/B-Testergebnisse in der Benutzeroberfläche von [!DNL Adobe Target] anzuzeigen, oder wählen Sie **[!UICONTROL Adobe Analytics]**, um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![alt image](assets/asset-reporting-b.png)

## 8. Hinzufügen von Metriken zur Verfolgung von KPIs

Wählen Sie eine **[!UICONTROL Goal Metric]** aus, um den Funktionstest mit Attributen zu messen. In diesem Beispiel basiert der Erfolg darauf, ob der Benutzer ein Produkt kauft, je nach dem angezeigten Sortieralgorithmus und der angezeigten Paginierungsstrategie.

## 9. Implementieren von Funktionstests mit Attributen in Ihre Anwendung

>[!BEGINTABS]

>[!TAB node.js]

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

>[!TAB Java]

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

>[!TAB node.js]

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

>[!TAB Java]

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

![alt image](assets/asset-activate.png)
