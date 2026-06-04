---
title: Ausführen von A/B-Tests mit Feature Flags und geräteinterner Entscheidungsfindung
description: Führen Sie A/B-Tests mit Feature Flags mithilfe der geräteinternen Entscheidungsfindung aus.
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
TQID: https://experienceleague.adobe.com/OnRFP7WgNvPy-9v8Ea8te3v5QAUlcR2WUlD7yGB-QzQ
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 813
ht-degree: 1%

---

# Ausführen von A/B-Tests mit Feature Flags

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL On-Device Decisioning] für Ihre Organisation
1. Erstellen einer [!UICONTROL A/B-Test]-Aktivität
1. A und B definieren
1. Hinzufügen einer Audience
1. Traffic-Zuordnung festlegen
1. Festlegen der Traffic-Verteilung auf Varianten
1. Einrichten von Berichten
1. Metriken für Tracking-KPIs hinzufügen
1. Implementieren von Code zum Ausführen von A/B-Tests mit Feature Flags
1. Aktivieren von A/B-Tests mit Feature Flags

>[!NOTE]
>
>Angenommen, Sie möchten ermitteln, ob Ihre Herbstumgestaltung Ihrer Homepage bei Ihren Nutzern gut ankommt. Sie können sie testen, indem Sie ein A/B-Experiment in [!DNL Adobe Target] durchführen. Sie sollten auch sicherstellen, dass das Experiment mit hoher Leistung durchgeführt wird, damit die Ergebnisse bei einem negativen oder langsamen Benutzererlebnis nicht verzerrt werden.

## &#x200B;1. Aktivieren [!UICONTROL On-Device Decisioning] für Ihre Organisation

Durch die Aktivierung der geräteinternen Entscheidungsfindung wird sichergestellt, dass eine A/B-Aktivität mit einer Latenz von nahezu null ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie **[!UICONTROL [!DNL Adobe Target] zu]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]**.

&lt;!— insert image-odd4.png —>
![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die Admin- oder Genehmiger[Benutzerrolle verfügen, &#x200B;](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=de) den Umschalter Geräteinterne Entscheidungsfindung zu aktivieren oder zu deaktivieren.

Nach der Aktivierung **[!UICONTROL Umschalters]** On-Device Decisioning“ beginnt [!DNL Adobe Target] mit der Generierung von Regelartefakten für Ihren Client.

## &#x200B;2. Erstellen einer [!UICONTROL A/B-Test]-Aktivität

Navigieren Sie in [!DNL Adobe Target] zur Seite **[!UICONTROL Aktivitäten]** und wählen Sie dann **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

![ALT-Bild](assets/asset-ab.png)

Lassen Sie im Modal **[!UICONTROL A/B-]** erstellen“ die Standardoption **[!UICONTROL Web]** ausgewählt (1), wählen Sie **[!UICONTROL Form]** als Experience Composer (2) aus, wählen Sie **[!UICONTROL Standard-Workspace]** ohne **[!UICONTROL Eigenschaftsbeschränkungen]** (3) aus und klicken Sie auf **[!UICONTROL Weiter]** (4).

![ALT-Bild](assets/asset-form.png)

## &#x200B;3. A und B definieren

1. Geben **[!UICONTROL im Schritt]** Erlebnisse“ der Aktivitätserstellung einen Namen für Ihre Aktivität ein (1) und fügen Sie ein zweites Erlebnis hinzu, Erlebnis B, indem Sie auf die Schaltfläche **[!UICONTROL Erlebnis hinzufügen]** (2) klicken. Geben Sie den Namen des Speicherorts (3) in Ihrer Anwendung ein, an dem Sie Ihren A/B-Test durchführen möchten. Im folgenden Beispiel ist „homepage“ der für Erlebnis A definierte Speicherort. (Es ist auch der für Erlebnis B definierte Speicherort.)

   Erlebnis A definiert das Steuerelement, d. h. das aktuelle Homepage-Design.

   ![ALT-Bild](assets/asset-exp-a.png)

   Erlebnis B definiert den Challenger, der eine neu gestaltete Homepage darstellt. Klicken, um Standardinhalt zu ändern (1).

   ![ALT-Bild](assets/asset-exp-b.png)

1. Klicken Sie in Erlebnis B auf , um den Inhalt von **[!UICONTROL Standardinhalt]** in den neu gestalteten Inhalt zu ändern, indem Sie **[!UICONTROL JSON-Angebot erstellen]** wie unten dargestellt (1) auswählen.

   ![ALT-Bild](assets/asset-offer.png)

1. Definieren Sie die JSON-Datei mit Attributen, die als Flags verwendet werden, damit Ihre Geschäftslogik die neu gestaltete Homepage anstatt die aktuelle Homepage in der Produktion rendern kann.


   >[!NOTE]
   >
   >Wenn [!DNL Adobe Target] einen Benutzer gruppiert, um Erlebnis B (die neu gestaltete Homepage) zu sehen, wird die JSON mit den im Beispiel definierten Attributen zurückgegeben. In Ihrem Code müssen Sie die Attributwerte überprüfen, um zu entscheiden, ob die Geschäftslogik zum Rendern der neu gestalteten Homepage ausgeführt werden soll. Sie können die Namen, Werte und die Anzahl der Attribute in dieser JSON-Antwort definieren.

   ![ALT-Bild](assets/asset-homepage.png)

## &#x200B;4. Hinzufügen einer Audience

Angenommen, Sie möchten das Redesign zunächst an Ihren treuen Kunden testen, die Sie identifizieren können, je nachdem, ob sie angemeldet sind oder nicht.

1. Klicken Sie **[!UICONTROL Schritt]** Targeting“, um die Zielgruppe **[!UICONTROL Alle Besucher]** zu ersetzen, wie dargestellt.

   ![ALT-Bild](assets/asset-all-audiences.png)

1. Definieren Sie **[!UICONTROL Modal &quot;]** erstellen“ eine benutzerdefinierte Regel, in der `logged-in = true` wird. Dies definiert die Gruppe der angemeldeten Benutzer. Diese Zielgruppe in Ihrer Aktivität verwenden.

   ![ALT-Bild](assets/asset-audience.png)

## &#x200B;5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz der angemeldeten Benutzer, mit denen Sie Ihr neues Homepage-Redesign testen möchten. Mit anderen Worten, zu welchem Prozentsatz der Benutzer möchten Sie diesen Test durchführen? Um diesen Test in diesem Beispiel für alle angemeldeten Benutzer bereitzustellen, sollten Sie die Traffic-Zuordnung bei 100 % belassen.

![ALT-Bild](assets/asset-allocation.png)

## &#x200B;6. Festlegen der Traffic-Verteilung auf Varianten

Definieren Sie den Prozentsatz Ihrer angemeldeten Benutzer, die das aktuelle Design der Homepage oder das komplett neue Redesign sehen werden. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![ALT-Bild](assets/asset-traffic-distribution.png)

## &#x200B;7. Einrichten von Berichten

Wählen Sie im Schritt **[!UICONTROL Ziele und Einstellungen]** die Option **[!UICONTROL Adobe Target]** als **[!UICONTROL Reporting-Source]** aus, um Aktivitätsergebnisse in der [!DNL Adobe Target]-Benutzeroberfläche anzuzeigen, oder wählen Sie **[!UICONTROL Adobe Analytics]** aus, um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![ALT-Bild](assets/asset-reporting.png)

## &#x200B;8. Metriken für Tracking-KPIs hinzufügen

Wählen Sie eine **[!UICONTROL Zielmetrik]**, um den A/B-Test zu messen. In diesem Beispiel basiert eine erfolgreiche Konversion darauf, ob der Benutzer das Seitenende erreicht, was auf eine Interaktion hinweist. Daher wird **[!UICONTROL Konversion]** danach bestimmt, ob der Benutzer den Ort mit dem Namen „Seitenende“ angesehen hat.

## &#x200B;9. Implementieren Sie Code zum Ausführen von A/B-Tests mit Feature Flags in Ihrer Anwendung

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
  return targetClient.getAttributes(["homepage"]).then(function(attributes) {
    const flag = attributes.getValue("homepage", "feature-flag");
    // ...
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
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "homepage");
String flag = attributes.getString("homepage", "feature-flag");
```

>[!ENDTABS]

## &#x200B;10. Aktivieren des A/B-Tests mit Feature Flag

![ALT-Bild](assets/asset-activate.png)
