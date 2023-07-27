---
title: Durchführen von A/B-Tests mit Funktionsmarkierungen und Entscheidungsfindung auf dem Gerät
description: Führen Sie A/B-Tests mit Funktionsmarkierungen durch, indem Sie die Entscheidungsfindung auf dem Gerät verwenden.
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Durchführen von A/B-Tests mit Funktionsmarkierungen

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation
1. Erstellen Sie eine [!UICONTROL A/B-Test] activity
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
>Angenommen, Sie möchten feststellen, ob Ihre Benutzer Ihre gestürzte Umgestaltung Ihrer Homepage gut empfangen. Sie entscheiden sich, sie zu testen, indem Sie ein A/B-Experiment in [!DNL Adobe Target]. Außerdem sollten Sie sicherstellen, dass das Experiment mit einer hervorragenden Leistung durchgeführt wird, damit ein negatives oder langsamen Benutzererlebnis die Ergebnisse nicht verfälscht.

## 1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** in [!DNL Adobe Target]und aktivieren Sie die **[!UICONTROL On-Device Decisioning]** umschalten.

&lt;!— Fügen Sie image-odd4.png —>
![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über einen Administrator oder Genehmiger verfügen. [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um den Umschalter On-Device Decisioning zu aktivieren oder zu deaktivieren.

Nach der Aktivierung der **[!UICONTROL On-Device Decisioning]** Umschalten, [!DNL Adobe Target] beginnt mit der Generierung von Regelartefakten für Ihren Client.

## 2. Erstellen Sie eine [!UICONTROL A/B-Test] activity

In [!DNL Adobe Target], navigieren Sie zum **[!UICONTROL Tätigkeiten]** Seite und wählen Sie **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

![ALT-Bild](assets/asset-ab.png)

Im **[!UICONTROL A/B-Test-Aktivität erstellen]** modal, Behalten Sie die Standardeinstellung bei **[!UICONTROL Web]** ausgewählte Option (1), wählen Sie **[!UICONTROL Formular]** Wählen Sie als Experience Composer (2) **[!UICONTROL Standardarbeitsbereich]** mit Nein **[!UICONTROL Eigenschaftenbeschränkungen]** (3) und klicken Sie auf **[!UICONTROL Nächste]** 4.

![ALT-Bild](assets/asset-form.png)

## 3. Definieren Sie Ihre A und B

1. Im **[!UICONTROL Erlebnisse]** Schritt der Aktivitätserstellung einen Namen für Ihre Aktivität angeben (1) und ein zweites Erlebnis, Erlebnis B, hinzufügen, indem Sie auf die **[!UICONTROL Erlebnis hinzufügen]** (2). Geben Sie den Namen des Orts (3) in Ihrer Anwendung ein, an dem Sie Ihren A/B-Test durchführen möchten. Im unten gezeigten Beispiel ist die Homepage der für Erlebnis A definierte Ort (sie ist auch der für Erlebnis B definierte Ort).

   Erlebnis A definiert das Steuerelement, das das aktuelle Startseitendesign ist.

   ![ALT-Bild](assets/asset-exp-a.png)

   Erlebnis B definiert den Challenger, der eine neu gestaltete Homepage darstellt. Klicken Sie auf , um den Standardinhalt zu ändern (1).

   ![ALT-Bild](assets/asset-exp-b.png)

1. Klicken Sie in Erlebnis B auf , um den Inhalt zu ändern von **[!UICONTROL Standardinhalt]** zum neu gestalteten Inhalt durch Auswahl von **[!UICONTROL JSON-Angebot erstellen]** wie unten gezeigt (1).

   ![ALT-Bild](assets/asset-offer.png)

1. Definieren Sie die JSON-Datei mit Attributen, die als Flags verwendet werden, damit Ihre Geschäftslogik die neu entworfene Homepage rendern kann und nicht die aktuelle Homepage in der Produktion.


   >[!NOTE]
   >
   >Wann [!DNL Adobe Target] erfasst einen Benutzer, um Erlebnis B (die neu gestaltete Homepage) zu sehen, wird die JSON mit den im Beispiel definierten Attributen zurückgegeben. In Ihrem Code müssen Sie die Attributwerte überprüfen, um zu entscheiden, ob die Geschäftslogik zum Rendern der neu gestalteten Homepage ausgeführt werden soll. Sie müssen die Namen, Werte und die Anzahl der Attribute in dieser JSON-Antwort definieren.

   ![ALT-Bild](assets/asset-homepage.png)

## 4. Audience hinzufügen

Angenommen, Sie möchten das Neudesign zunächst bei Ihren treuen Kunden testen, die Sie anhand dessen identifizieren können, ob sie angemeldet sind oder nicht.

1. Im **[!UICONTROL Targeting]** klicken Sie auf , um die **[!UICONTROL Alle Besucher]** Zielgruppe, wie dargestellt.

   ![ALT-Bild](assets/asset-all-audiences.png)

1. Im **[!UICONTROL Zielgruppe erstellen]** modal definieren, definieren Sie eine benutzerdefinierte Regel, bei der `logged-in = true`. Dadurch wird die Gruppe der angemeldeten Benutzer definiert. Verwenden Sie diese Zielgruppe in Ihrer Aktivität.

   ![ALT-Bild](assets/asset-audience.png)

## 5. Traffic-Zuordnung festlegen

Definieren Sie den Prozentsatz der angemeldeten Benutzer, mit denen Sie die Neugestaltung Ihrer neuen Homepage testen möchten. Mit anderen Worten, zu welchem Prozentsatz Ihrer Benutzer möchten Sie diesen Test einführen? Um diesen Test für alle angemeldeten Benutzer bereitzustellen, halten Sie die Traffic-Zuordnung in diesem Beispiel bei 100 %.

![ALT-Bild](assets/asset-allocation.png)

## 6. Traffic-Verteilung auf Varianten festlegen

Definieren Sie den Prozentsatz Ihrer angemeldeten Benutzer, der das aktuelle Design der Homepage oder die völlig neue Neugestaltung sieht. Behalten Sie in diesem Beispiel die Traffic-Verteilung als 50/50-Aufteilung zwischen den Erlebnissen A und B bei.

![ALT-Bild](assets/asset-traffic-distribution.png)

## 7. Einrichten von Berichten

Im **[!UICONTROL Ziele und Einstellungen]** Schritt auswählen **[!UICONTROL Adobe Target]** als **[!UICONTROL Berichtsquelle]** um die Aktivitätsergebnisse in der [!DNL Adobe Target] Benutzeroberfläche oder wählen Sie **[!UICONTROL Adobe Analytics]** , um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![ALT-Bild](assets/asset-reporting.png)

## 8. Hinzufügen von Metriken zur Verfolgung von KPIs

Wählen Sie eine **[!UICONTROL Zielmetrik]** , um den A/B-Test zu messen. In diesem Beispiel basiert eine erfolgreiche Konversion darauf, ob der Benutzer den unteren Seitenrand erreicht, was die Interaktion angibt. Daher **[!UICONTROL Konversion]** wird anhand der Tatsache bestimmt, ob der Benutzer den Ort unten auf der Seite angezeigt hat.

## 9. Implementieren Sie Code, um A/B-Tests mit Funktionsmarkierungen in Ihre Anwendung auszuführen.

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

![ALT-Bild](assets/asset-activate.png)
