---
title: Ausführen von Funktionstests mit Attributen
description: Ausführen von Funktionstests mit Attributen
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
TQID: https://experienceleague.adobe.com/y2Mwmnn2k91-LKBy1UmZ5a1s6dZeb5VMyHdyJc2lc34
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 960
ht-degree: 1%

---

# Ausführen von Funktionstests mit Attributen

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL On-Device Decisioning] für Ihre Organisation
1. Erstellen einer [!UICONTROL A/B-Test]-Aktivität
1. A und B definieren
1. Hinzufügen einer Audience
1. Traffic-Zuordnung festlegen
1. Festlegen der Traffic-Verteilung auf Varianten
1. Einrichten von Berichten
1. Metriken für Tracking-KPIs hinzufügen
1. Implementieren von Code zum Ausführen von Funktionstests mit Attributen
1. Implementieren von Code zum Tracking von Konversionsereignissen
1. Aktivieren von Funktionstests mit Attributen

>[!NOTE]
>
>Angenommen, Sie sind ein E-Commerce-Einzelhandelsunternehmen. Sie möchten die Konversionsrate erhöhen, wenn Kunden Ihren Produktkatalog durchsuchen und sortieren. Sie haben die Hypothese, dass bestimmte Sortieralgorithmen und Paginierungsstrategien bessere Ergebnisse liefern als andere. Um diese Theorie zu testen, führen Sie einen Funktionstest durch, bei dem das Sortier-Widget mit verschiedenen Sortieroptionen für Ihre Endbenutzenden neu gestaltet wird. Sie sollten sicherstellen, dass dieser Funktionstest mit einer Latenz nahe null ausgeführt wird, damit die Benutzererfahrung nicht beeinträchtigt wird und die Ergebnisse nicht verzerrt werden.

## &#x200B;1. Aktivieren [!UICONTROL On-Device Decisioning] für Ihre Organisation

Durch die Aktivierung der geräteinternen Entscheidungsfindung wird sichergestellt, dass eine A/B-Aktivität mit einer Latenz von nahezu null ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie **[!UICONTROL [!DNL Adobe Target] zu]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]**.

![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die Admin- oder Genehmiger[Benutzerrolle verfügen, &#x200B;](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren oder zu deaktivieren.

Nach der Aktivierung **[!UICONTROL Umschalters]** On-Device Decisioning“ beginnt [!DNL Adobe Target] mit der Erstellung *Regelartefakte* für Ihren Client.

## &#x200B;2. Erstellen einer [!UICONTROL A/B-Test]-Aktivität

1. Navigieren Sie in [!DNL Adobe Target] zur Seite **[!UICONTROL Aktivitäten]** und wählen Sie dann **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

   ![ALT-Bild](assets/asset-ab.png)

1. Lassen Sie im Modal **[!UICONTROL A/B-]** erstellen“ die Standardoption **[!UICONTROL Web]** ausgewählt (1), wählen Sie **[!UICONTROL Form]** als Experience Composer (2) aus, wählen Sie **[!UICONTROL Standard-Workspace]** mit **[!UICONTROL Keine Eigenschaftsbeschränkungen]** (3) aus und klicken Sie auf **[!UICONTROL Weiter]** (4).

   ![ALT-Bild](assets/asset-form.png)

## &#x200B;3. A und B definieren

1. Geben **[!UICONTROL im Schritt]** Erlebnisse“ der Aktivitätserstellung einen Namen für Ihre Aktivität ein (1) und fügen Sie ein zweites Erlebnis hinzu, Erlebnis B, indem Sie auf die Schaltfläche **[!UICONTROL Erlebnis hinzufügen]** (2) klicken. Geben Sie den Namen des Speicherorts (3) innerhalb Ihrer Anwendung ein, an dem Sie Ihren Funktionstest mit Attributen ausführen möchten. Im folgenden Beispiel ist `product-results-page` der für Erlebnis A definierte Speicherort. (Es ist auch der für Erlebnis B definierte Speicherort.)

   ![ALT-Bild](assets/asset-location.png)

   **[!UICONTROL Erlebnis A]** enthält die JSON-Datei, die Ihrer Geschäftslogik signalisiert, Folgendes zu tun:

   * Starten Sie die Sortieralgorithmus-Funktion über das Feature Flag &quot;`test_sorting`&quot;
   * Ausführen des im `sorting_algorithm _**_attribute` definierten empfohlenen Sortieralgorithmus
   * Gibt 50 Produkte pro Seite zurück, wie durch die in der `pagination_limit` definierte Paginierungsstrategie definiert

1. Klicken Sie in Erlebnis A auf , um den Inhalt von **[!UICONTROL Standardinhalt]** in JSON zu ändern, indem Sie **[!UICONTROL JSON-Angebot erstellen]** wie unten dargestellt (1) auswählen.

   ![ALT-Bild](assets/asset-offer.png)

1. Definieren Sie die JSON-Datei mit `test_sorting`-, `sorting_algorithm`- und `pagination_limit`-Flags und -Attributen, die zum Initiieren des empfohlenen Sortieralgorithmus mit einer Paginierungsgrenze von 50 Produkten verwendet werden.

   >[!NOTE]
   >
   >Wenn ein Benutzer [!DNL Adobe Target] wird, um Erlebnis A zu sehen, wird die JSON mit den im Beispiel definierten Attributen zurückgegeben. In Ihrem Code müssen Sie den Wert der Feature Flag-`test_sorting` überprüfen, um festzustellen, ob die Sortierfunktion aktiviert werden soll. In diesem Fall verwenden Sie den empfohlenen Wert des Attributs `sorting_algorithm` , um empfohlene Produkte in der Produktlistenansicht anzuzeigen. Die maximale Anzahl von Produkten, die für Ihre Anwendung angezeigt werden können, beträgt 50, da dies der Wert des Attributs `pagination_limit` ist.

   ![ALT-Bild](assets/asset-sorting.png)

   **[!UICONTROL Erlebnis B]** definiert die JSON, die Ihrer Geschäftslogik signalisiert, Folgendes zu tun:

   * Starten Sie die Sortieralgorithmusfunktion über das Feature Flag test_sort .
   * Führen Sie den im `sorting_algorithm _**_attribute` definierten `best_sellers` aus
   * Gibt 50 Produkte pro Seite zurück, wie durch die in der `pagination_limit` definierte Paginierungsstrategie definiert

   >[!NOTE]
   >
   >Wenn ein Benutzer [!DNL Adobe Target] wird, um Erlebnis B zu sehen, wird die JSON mit den im Beispiel definierten Attributen zurückgegeben. In Ihrem Code müssen Sie den Wert der Feature Flag-`test_sorting` überprüfen, um festzustellen, ob die Sortierfunktion aktiviert werden soll. In diesem Fall verwenden Sie den `best_sellers` des Attributs `sorting_algorithm` , um die meistverkauften Produkte in der Produktlistenansicht anzuzeigen. Die maximale Anzahl von Produkten, die für Ihre Anwendung angezeigt werden können, beträgt 50, da dies der Wert des Attributs `pagination_limit` ist.

   ![ALT-Bild](assets/asset-sorting-b.png)

## &#x200B;4. Hinzufügen einer Audience

Behalten **[!UICONTROL Schritt]** Targeting“ die Zielgruppe **[!UICONTROL Alle Besucher]** bei. Auf diese Weise können Sie die Auswirkungen Ihrer Sortierfunktion verstehen und feststellen, welcher Algorithmus und welche Anzahl von Elementen die Ergebnisse am besten beeinflussen.

![ALT-Bild](assets/asset-audience-b.png)

## &#x200B;5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz Ihrer Besucher, mit denen Sie Ihre Sortieralgorithmen und Ihre Paginierungsstrategie testen möchten. Mit anderen Worten, zu welchem Prozentsatz der Benutzer möchten Sie diesen Test durchführen? Um diesen Test in diesem Beispiel für alle angemeldeten Benutzer bereitzustellen, sollten Sie die Traffic-Zuordnung bei 100 % belassen.

![ALT-Bild](assets/asset-allocation-100.png)

## &#x200B;6. Festlegen der Traffic-Verteilung auf Varianten

Definieren Sie den Prozentsatz Ihrer Besucher, die den empfohlenen Sortieralgorithmus im Vergleich zum Best-Sellers-Sortieralgorithmus sehen, mit einer Beschränkung von 50 Produkten pro Seite. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![ALT-Bild](assets/asset-variations-50.png)

## &#x200B;7. Einrichten von Berichten

Wählen Sie im Schritt **[!UICONTROL Ziele und Einstellungen]** die Option **[!UICONTROL Adobe Target]** als **[!UICONTROL Reporting-Source]** aus, um Ihre A/B-Testergebnisse in der [!DNL Adobe Target]-Benutzeroberfläche anzuzeigen, oder wählen Sie **[!UICONTROL Adobe Analytics]** aus, um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![ALT-Bild](assets/asset-reporting-b.png)

## &#x200B;8. Metriken für Tracking-KPIs hinzufügen

Wählen Sie eine **[!UICONTROL Zielmetrik]**, um den Funktionstest mit Attributen zu messen. In diesem Beispiel hängt der Erfolg davon ab, ob der Benutzer ein Produkt kauft, je nach dem Sortieralgorithmus und der Paginierungsstrategie, die er angezeigt hat.

## &#x200B;9. Implementieren von Funktionstests mit Attributen in Ihr Programm

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

## &#x200B;10. Implementieren von Code zum Tracking von Konversionsereignissen

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

## &#x200B;11. Aktivieren von Funktionstests mit Attributen

![ALT-Bild](assets/asset-activate.png)
