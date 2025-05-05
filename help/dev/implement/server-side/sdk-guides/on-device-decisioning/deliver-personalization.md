---
title: Bereitstellen von Personalisierung mit Adobe Target SDKs
description: Erfahren Sie, wie Sie mithilfe von [!UICONTROL on-device decisioning] Personalisierung bereitstellen können.
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Personalisierung bereitstellen

## Zusammenfassung der Schritte

1. Aktivieren von [!UICONTROL on-device decisioning] für Ihr Unternehmen
1. Erstellen einer [!UICONTROL Experience Targeting] (XT)-Aktivität
1. Definieren personalisierter Erlebnisse pro Zielgruppe
1. Überprüfen personalisierter Erlebnisse pro Zielgruppe
1. Einrichten von Berichten
1. Metriken für Tracking-KPIs hinzufügen
1. Personalisierte Angebote in Ihrer Anwendung implementieren
1. Implementieren von Code zum Tracking von Konversionsereignissen
1. Aktivieren der [!UICONTROL Experience Targeting] (XT)-Personalisierungsaktivität

Angenommen, Sie sind ein Reiseunternehmen. Sie möchten ein personalisiertes Angebot von 25% Rabatt auf bestimmte Reisepakete anbieten. Damit das Angebot bei Ihren Nutzern Anklang findet, entscheiden Sie sich, ein Wahrzeichen der Zielstadt anzuzeigen. Sie sollten auch sicherstellen, dass die Bereitstellung Ihrer personalisierten Angebote mit einer Latenz nahe null erfolgt, damit die Benutzererlebnisse nicht beeinträchtigt werden und die Ergebnisse nicht verzerrt werden.

## 1. Aktivieren von [!UICONTROL on-device decisioning] für Ihr Unternehmen

1. Durch die Aktivierung der geräteinternen Entscheidungsfindung wird sichergestellt, dass eine A/B-Aktivität mit einer Latenz von nahezu null ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie in [!DNL Adobe Target] zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

   ![ALT-Bild](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >Sie müssen über die Rolle Administrator oder Genehmiger [Benutzer) verfügen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=de) um den Umschalter [!UICONTROL On-Device Decisioning] zu aktivieren oder zu deaktivieren.

   Nach der Aktivierung des **[!UICONTROL On-Device Decisioning]**-Umschalters beginnt [!DNL Adobe Target] mit der Generierung *Regelartefakte* für Ihren Client.

## 2. Erstellen einer [!UICONTROL Experience Targeting] (XT)-Aktivität

1. Navigieren Sie in [!DNL Adobe Target] zur Seite **[!UICONTROL Activities]** und wählen Sie dann **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]** aus.

   ![ALT-Bild](assets/asset-xt.png)

1. Lassen Sie im **[!UICONTROL Create Experience Targeting Activity]**-Modal die Option **[!UICONTROL Web]** ausgewählt (1), wählen Sie **[!UICONTROL Form]** als Experience Composer (2), wählen Sie einen Arbeitsbereich und eine Eigenschaft aus (3) und klicken Sie auf **[!UICONTROL Next]** (4).

   ![ALT-Bild](assets/asset-xt-next.png)

## 3. Definieren eines personalisierten Erlebnisses pro Zielgruppe

1. Klicken Sie im **[!UICONTROL Experiences]** Schritt der Aktivitätserstellung auf **[!UICONTROL Change Audience]** , um eine Zielgruppe derjenigen Besucher zu erstellen, die nach San Francisco, Kalifornien reisen möchten.

   ![ALT-Bild](assets/asset-change-audience.png)

1. Definieren Sie im **[!UICONTROL Create Audience]**-Modal eine benutzerdefinierte Regel, in der `destinationCity = San Francisco` ist. Diese Gruppe definiert die Benutzenden, die nach San Francisco reisen möchten.

   ![ALT-Bild](assets/asset-audience-sf.png)

1. Geben Sie noch im **[!UICONTROL Experiences]** Schritt den Namen des Ortes (1) in Ihrer Anwendung ein, an dem Sie ein Sonderangebot für das Golden Gate Bridge machen möchten, jedoch nur für diejenigen, die nach San Francisco fahren. In dem hier gezeigten Beispiel ist die Homepage der Ort, der für das HTML-Angebot (2) ausgewählt wurde und im **[!UICONTROL Content]** definiert ist.

   ![ALT-Bild](assets/asset-content-sf.png)

1. Fügen Sie eine weitere Zielgruppe hinzu, indem Sie auf **[!UICONTROL Add Experience Targeting]** klicken. Dieses Mal sollten Sie eine Zielgruppe ansprechen, die nach New York reisen möchte, indem Sie eine Zielgruppenregel definieren, bei der `destinationCity = New York` gilt. Definieren Sie in Ihrem Programm den Ort, an dem Sie ein Sonderangebot für das Empire State Building unterbreiten möchten. In dem hier gezeigten Beispiel ist `homepage` der Ort, der für das HTML-Angebot (2) ausgewählt wurde und im **[!UICONTROL Content]** definiert ist.

   ![ALT-Bild](assets/asset-content-ny.png)

## 4. Überprüfen des personalisierten Erlebnisses pro Zielgruppe

Stellen Sie im **[!UICONTROL Targeting]** Schritt sicher, dass Sie das gewünschte personalisierte Erlebnis pro Zielgruppe konfiguriert haben.

![ALT-Bild](assets/asset-verify-sf-ny.png)

## 5. Einrichten von Berichten

Wählen Sie im **[!UICONTROL Goals & Settings]** Schritt **[!UICONTROL Adobe Target]** als **[!UICONTROL Reporting Source]** aus, um die Aktivitätsergebnisse in der [!DNL Adobe Target] Benutzeroberfläche anzuzeigen, oder wählen Sie **[!UICONTROL Adobe Analytics]** aus, um sie in der Benutzeroberfläche von Adobe Analytics anzuzeigen.

![ALT-Bild](assets/asset-reporting-sf-ny.png)

## 6. Hinzufügen von Metriken für Tracking-KPIs

Wählen Sie eine **[!UICONTROL Goal Metric]** aus, um den Erfolg der Aktivität zu messen. In diesem Beispiel basiert eine erfolgreiche Konversion darauf, ob der Benutzer auf das personalisierte Zielangebot klickt.

## 7. Personalisierte Angebote in der Anwendung implementieren

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {      
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
    }       
  }
})
.then(console.log)
.catch(console.error);
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

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 8. Implementieren von Code zum Tracking von Konversionsereignissen

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
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
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
```

>[!ENDTABS]

## 9. Aktivieren Sie Ihre Experience Targeting-(XT)-Aktivität

![ALT-Bild](assets/asset-xt-activate.png)
