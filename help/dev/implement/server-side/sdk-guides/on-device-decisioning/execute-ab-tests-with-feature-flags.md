---
title: Durchführen von A/B-Tests mit Funktionsmarkierungen und Entscheidungsfindung auf dem Gerät
description: Führen Sie A/B-Tests mit Funktionsmarkierungen durch, indem Sie die Entscheidungsfindung auf dem Gerät verwenden.
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Durchführen von A/B-Tests mit Funktionsmarkierungen

## Zusammenfassung der Schritte

1. [!UICONTROL on-device decisioning] für Ihre Organisation aktivieren
1. Erstellen einer [!UICONTROL A/B Test] -Aktivität
1. A und B definieren
1. Hinzufügen einer Zielgruppe
1. Traffic-Zuordnung festlegen
1. Traffic-Verteilung auf Varianten festlegen
1. Berichterstellung einrichten
1. Metriken zur Verfolgung von KPIs hinzufügen
1. Implementieren von Code zum Ausführen von A/B-Tests mit Funktionsmarkierungen
1. Aktivieren Ihres A/B-Tests mit Funktionsmarkierungen

>[!NOTE]
>
>Angenommen, Sie möchten feststellen, ob Ihre Benutzer Ihre gestürzte Umgestaltung Ihrer Homepage gut empfangen. Sie entscheiden sich, sie durch Ausführen eines A/B-Experiments in [!DNL Adobe Target] zu testen. Außerdem sollten Sie sicherstellen, dass das Experiment mit einer hervorragenden Leistung durchgeführt wird, damit ein negatives oder langsamen Benutzererlebnis die Ergebnisse nicht verfälscht.

## 1. Aktivieren Sie [!UICONTROL on-device decisioning] für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie in [!DNL Adobe Target] zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

&lt;!— Fügen Sie image-odd4.png —>
![alt image](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die Benutzerrolle &quot;Admin&quot;oder &quot;Genehmiger&quot;[Benutzer](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) verfügen, um den Umschalter &quot;On-Device Decisioning&quot;zu aktivieren oder zu deaktivieren.

Nachdem Sie den Umschalter **[!UICONTROL On-Device Decisioning]** aktiviert haben, beginnt [!DNL Adobe Target] mit der Generierung von Regelartefakten für Ihren Client.

## 2. Erstellen einer [!UICONTROL A/B Test] -Aktivität

Navigieren Sie in [!DNL Adobe Target] zur Seite **[!UICONTROL Activities]** und wählen Sie dann **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]** aus.

![alt image](assets/asset-ab.png)

Behalten Sie im Modal **[!UICONTROL Create A/B Test Activity]** die standardmäßig ausgewählte Option **[!UICONTROL Web]** bei (1), wählen Sie **[!UICONTROL Form]** als Ihren Experience Composer (2), wählen Sie **[!UICONTROL Default Workspace]** mit Nein **[!UICONTROL Property Restrictions]** (3) aus und klicken Sie auf **[!UICONTROL Next]** (4).

![alt image](assets/asset-form.png)

## 3. Definieren Sie Ihre A und B

1. Geben Sie im Schritt **[!UICONTROL Experiences]** der Aktivitätserstellung einen Namen für Ihre Aktivität (1) ein und fügen Sie ein zweites Erlebnis, Erlebnis B, hinzu, indem Sie auf die Schaltfläche **[!UICONTROL Add Experience]** (2) klicken. Geben Sie den Namen des Orts (3) in Ihrer Anwendung ein, an dem Sie Ihren A/B-Test durchführen möchten. Im unten gezeigten Beispiel ist die Homepage der für Erlebnis A definierte Ort (sie ist auch der für Erlebnis B definierte Ort).

   Erlebnis A definiert das Steuerelement, das das aktuelle Startseitendesign ist.

   ![alt image](assets/asset-exp-a.png)

   Erlebnis B definiert den Challenger, der eine neu gestaltete Homepage darstellt. Klicken Sie auf , um den Standardinhalt zu ändern (1).

   ![alt image](assets/asset-exp-b.png)

1. Klicken Sie in Erlebnis B auf , um den Inhalt von **[!UICONTROL Default Content]** in den neu gestalteten Inhalt zu ändern, indem Sie **[!UICONTROL Create JSON Offer]** wie unten gezeigt (1) auswählen.

   ![alt image](assets/asset-offer.png)

1. Definieren Sie die JSON-Datei mit Attributen, die als Flags verwendet werden, damit Ihre Geschäftslogik die neu entworfene Homepage rendern kann und nicht die aktuelle Homepage in der Produktion.


   >[!NOTE]
   >
   >Wenn [!DNL Adobe Target] einen Benutzer erfasst, um Erlebnis B (die neu gestaltete Homepage) anzuzeigen, wird die JSON mit den im Beispiel definierten Attributen zurückgegeben. In Ihrem Code müssen Sie die Attributwerte überprüfen, um zu entscheiden, ob die Geschäftslogik zum Rendern der neu gestalteten Homepage ausgeführt werden soll. Sie müssen die Namen, Werte und die Anzahl der Attribute in dieser JSON-Antwort definieren.

   ![alt image](assets/asset-homepage.png)

## 4. Audience hinzufügen

Angenommen, Sie möchten das Neudesign zunächst bei Ihren treuen Kunden testen, die Sie anhand dessen identifizieren können, ob sie angemeldet sind oder nicht.

1. Klicken Sie im Schritt &quot;**[!UICONTROL Targeting]**&quot;auf , um die &quot;**[!UICONTROL All Visitors]**&quot;-Zielgruppe zu ersetzen, wie unten dargestellt.

   ![alt image](assets/asset-all-audiences.png)

1. Definieren Sie im Modal **[!UICONTROL Create Audience]** eine benutzerdefinierte Regel mit dem Wert `logged-in = true`. Dadurch wird die Gruppe der angemeldeten Benutzer definiert. Verwenden Sie diese Zielgruppe in Ihrer Aktivität.

   ![alt image](assets/asset-audience.png)

## 5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz der angemeldeten Benutzer, mit denen Sie die Neugestaltung Ihrer neuen Homepage testen möchten. Mit anderen Worten, zu welchem Prozentsatz Ihrer Benutzer möchten Sie diesen Test einführen? Um diesen Test für alle angemeldeten Benutzer bereitzustellen, halten Sie die Traffic-Zuordnung in diesem Beispiel bei 100 %.

![alt image](assets/asset-allocation.png)

## 6. Traffic-Verteilung auf Varianten festlegen

Definieren Sie den Prozentsatz Ihrer angemeldeten Benutzer, der das aktuelle Design der Homepage oder die völlig neue Neugestaltung sieht. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![alt image](assets/asset-traffic-distribution.png)

## 7. Einrichten von Berichten

Wählen Sie im Schritt **[!UICONTROL Goals & Settings]** die Option **[!UICONTROL Adobe Target]** als den Wert **[!UICONTROL Reporting Source]**, um die Aktivitätsergebnisse in der Benutzeroberfläche von [!DNL Adobe Target] anzuzeigen, oder wählen Sie **[!UICONTROL Adobe Analytics]**, um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![alt image](assets/asset-reporting.png)

## 8. Hinzufügen von Metriken zur Verfolgung von KPIs

Wählen Sie **[!UICONTROL Goal Metric]** aus, um den A/B-Test zu messen. In diesem Beispiel basiert eine erfolgreiche Konversion darauf, ob der Benutzer den unteren Seitenrand erreicht, was die Interaktion angibt. Daher wird **[!UICONTROL Conversion]** anhand der Tatsache bestimmt, ob der Benutzer den Ort namens unten auf der Seite angezeigt hat.

## 9. Implementieren Sie Code, um A/B-Tests mit Funktionsmarkierungen in Ihre Anwendung auszuführen.

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

## 10. Aktivieren Sie Ihren A/B-Test mit Feature Flag

![alt image](assets/asset-activate.png)
