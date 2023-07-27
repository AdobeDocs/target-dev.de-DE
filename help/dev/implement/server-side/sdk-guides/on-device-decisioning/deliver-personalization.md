---
title: Personalisierung mit Adobe Target SDKs bereitstellen
description: Erfahren Sie, wie Sie mithilfe von Personalisierung bereitstellen. [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Personalisierung bereitstellen

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation
1. Erstellen Sie eine [!UICONTROL Erlebnis-Targeting] (XT)-Aktivität
1. Definieren eines personalisierten Erlebnisses pro Zielgruppe
1. Überprüfen des personalisierten Erlebnisses pro Zielgruppe
1. Berichterstellung einrichten
1. Metriken zur Verfolgung von KPIs hinzufügen
1. Personalisierte Angebote in Ihre Anwendung implementieren
1. Implementieren von Code zur Verfolgung von Konversionsereignissen
1. Aktivieren Ihrer [!UICONTROL Erlebnis-Targeting] (XT) Personalisierungsaktivität

Nehmen wir an, Sie sind ein Tourenunternehmen. Sie möchten ein personalisiertes Angebot mit 25 % Rabatt auf bestimmte Reisepakete anbieten. Damit das Angebot bei Ihren Benutzern ankommt, möchten Sie ein Wahrzeichen der Zielstadt anzeigen. Sie möchten auch sicherstellen, dass die Bereitstellung Ihrer personalisierten Angebote mit einer Latenz von nahezu null ausgeführt wird, damit sich dies nicht negativ auf Benutzererlebnisse auswirkt und die Ergebnisse verfälscht.

## 1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation

1. Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** in [!DNL Adobe Target]und aktivieren Sie die **[!UICONTROL On-Device Decisioning]** umschalten.

   ![ALT-Bild](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >Sie müssen über einen Administrator oder Genehmiger verfügen. [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um die [!UICONTROL On-Device Decisioning] umschalten.

   Nach der Aktivierung der **[!UICONTROL On-Device Decisioning]** Umschalten, [!DNL Adobe Target] beginnt zu generieren *ruleArtefakte* für Ihren Client.

## 2. Erstellen Sie eine [!UICONTROL Erlebnis-Targeting] (XT)-Aktivität

1. In [!DNL Adobe Target], navigieren Sie zum **[!UICONTROL Tätigkeiten]** Seite und wählen Sie **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL Erlebnis-Targeting]**.

   ![ALT-Bild](assets/asset-xt.png)

1. Im **[!UICONTROL Erstellen einer Erlebnis-Targeting-Aktivität]** modal, Behalten Sie die Standardeinstellung bei **[!UICONTROL Web]** ausgewählte Option (1), wählen Sie **[!UICONTROL Formular]** als Experience Composer (2) einen Arbeitsbereich und eine Eigenschaft (3) auswählen und auf **[!UICONTROL Nächste]** 4.

   ![ALT-Bild](assets/asset-xt-next.png)

## 3. Personalisierte Erlebnisse pro Zielgruppe definieren

1. Im **[!UICONTROL Erlebnisse]** Schritt der Aktivitätserstellung, klicken Sie auf **[!UICONTROL Zielgruppe ändern]** , um eine Audience der Besucher zu erstellen, die nach San Francisco, Kalifornien, reisen möchten.

   ![ALT-Bild](assets/asset-change-audience.png)

1. Im **[!UICONTROL Zielgruppe erstellen]** modal definieren, definieren Sie eine benutzerdefinierte Regel, bei der `destinationCity = San Francisco`. Dies definiert die Gruppe von Benutzern, die nach San Francisco reisen möchten.

   ![ALT-Bild](assets/asset-audience-sf.png)

1. Noch im **[!UICONTROL Erlebnisse]** Geben Sie den Namen des Ortes (1) in Ihrer Anwendung ein, an dem Sie ein Sonderangebot für die Golden Gate Bridge rendern möchten, jedoch nur für diejenigen, die nach San Francisco fahren. In dem hier gezeigten Beispiel ist homepage der Ort, der für das HTML-Angebot (2) ausgewählt wurde, das im **[!UICONTROL Inhalt]** Bereich.

   ![ALT-Bild](assets/asset-content-sf.png)

1. Fügen Sie eine weitere Zielgruppe hinzu, indem Sie auf **[!UICONTROL Hinzufügen von Erlebnis-Targeting]**. Legen Sie dieses Mal eine Zielgruppe fest, die nach New York reisen möchte, indem Sie eine Zielgruppenregel definieren, in der `destinationCity = New York`. Definieren Sie den Ort in Ihrer Anwendung, an dem Sie ein Sonderangebot zum Empire State Building unterbreiten möchten. In dem hier gezeigten Beispiel: `homepage` der für das HTML-Angebot ausgewählte Ort (2), der in der Variablen **[!UICONTROL Inhalt]** Bereich.

   ![ALT-Bild](assets/asset-content-ny.png)

## 4. Überprüfen des personalisierten Erlebnisses pro Zielgruppe

Im **[!UICONTROL Targeting]** Schritt, überprüfen Sie, ob Sie das gewünschte personalisierte Erlebnis pro Zielgruppe konfiguriert haben.

![ALT-Bild](assets/asset-verify-sf-ny.png)

## 5. Einrichten von Berichten

Im **[!UICONTROL Ziele und Einstellungen]** Schritt auswählen **[!UICONTROL Adobe Target]** als **[!UICONTROL Berichtsquelle]** um die Aktivitätsergebnisse in der [!DNL Adobe Target] Benutzeroberfläche oder wählen Sie **[!UICONTROL Adobe Analytics]** , um sie in der Adobe Analytics-Benutzeroberfläche anzuzeigen.

![ALT-Bild](assets/asset-reporting-sf-ny.png)

## 6. Hinzufügen von Metriken zur Verfolgung von KPIs

Wählen Sie eine **[!UICONTROL Zielmetrik]** , um den Erfolg der Aktivität zu messen. In diesem Beispiel basiert eine erfolgreiche Konversion darauf, ob der Benutzer auf das personalisierte Zielangebot klickt.

## 7. Personalisierte Angebote in Ihre Anwendung implementieren

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

>[!TAB Java ]

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

## 8. Implementieren Sie Code zur Verfolgung von Konversionsereignissen

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

>[!TAB Java ]

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

## 9. Aktivität &quot;Erlebnis-Targeting&quot;(XT) aktivieren

![ALT-Bild](assets/asset-xt-activate.png)
