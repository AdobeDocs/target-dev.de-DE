---
title: Erste Schritte mit Target-SDKs
description: Wie verwende ich die Adobe Target SDKs?
feature: APIs/SDKs
exl-id: a5ae9826-7bb5-41de-8796-76edc4f5b281
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Erste Schritte mit [!DNL Target] SDKs

Damit Sie richtig arbeiten können, empfehlen wir Ihnen, Ihre erste [on-device decisioning](../on-device-decisioning/overview.md) Funktionsmarkierungsaktivität in der Sprache Ihrer Wahl:

* Node.js
* Java
* .NET
* Python

## Zusammenfassung der Schritte

1. Aktivieren der geräteübergreifenden Entscheidungsfindung für Ihre Organisation
1. SDK installieren
1. Initialisieren des SDK
1. Richten Sie die Funktionsmarkierungen in einem [!DNL Adobe Target] [!UICONTROL A/B-Test] activity
1. Funktion in Ihre Anwendung implementieren und rendern
1. Implementieren des Trackings für Ereignisse in Ihrer Anwendung
1. Aktivieren Ihrer [!UICONTROL A/B-Test] activity

## 1. Aktivieren Sie die Entscheidungsfindung auf dem Gerät für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird eine [!UICONTROL A/B-Test] -Aktivität wird mit einer Latenz von nahezu null ausgeführt. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** und aktivieren Sie die **[!UICONTROL On-Device Decisioning]** umschalten.

![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die **[!UICONTROL Admin]** oder **[!UICONTROL Genehmiger]** [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um die **[!UICONTROL On-Device Decisioning]** umschalten.

Nach der Aktivierung der **[!UICONTROL On-Device Decisioning]** Umschalten, [!DNL Adobe Target] beginnt zu generieren [ruleArtefakte](../on-device-decisioning/rule-artifact-overview.md) für Ihren Client.

## 2. Installieren des SDK

Führen Sie für Node.js, Java und Python den folgenden Befehl in Ihrem Projektverzeichnis im Terminal aus. Fügen Sie es für .NET als Abhängigkeit von [Installieren von NuGet](https://www.nuget.org/packages/Adobe.Target.Client).

>[!BEGINTABS]

>[!TAB Node.js (NPM)]

```js {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
<dependency>
   <groupId>com.adobe.target</groupId>
   <artifactId>java-sdk</artifactId>
   <version>2.0</version>
</dependency>
```

>[!TAB .NET (Bash)]

```bash {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!TAB Python (pip)]

```python {line-numbers="true"}
pip install target-python-sdk
```

>[!ENDTABS]

## 3. Initialisieren des SDK

Das Regelartefakt wird während des Initialisierungsschritts des SDK heruntergeladen. Sie können den Initialisierungsschritt anpassen, um zu bestimmen, wie das Artefakt heruntergeladen und verwendet wird.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
   client: "<your target client code>",
   organizationId: "your EC org id",
   decisioningMethod: "on-device",
   events: {
      clientReady: targetClientReady
      }
};

const tClient = TargetClient.create(CONFIG);

function targetClientReady() {
   //Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   //We will see how to use the artifact here very soon.
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
   .client("testClient")
   .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
   .build();
TargetClient targetClient = TargetClient.create(config);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("testClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
   .Build();
this.targetClient.Initialize(targetClientConfig);
```

>[!TAB Python]

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def target_client_ready():
   # Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   # We will see how to use the artifact here very soon.

CONFIG = {
   "client": "<your target client code>",
   "organization_id": "your EC org id",
   "decisioning_method": "on-device",
   "events": {
      "client_ready": target_client_ready
   }
}

target_client = TargetClient.create(CONFIG)
```

>[!ENDTABS]

## 4. Richten Sie die Feature Flags in ein [!DNL Adobe Target] [!UICONTROL A/B-Test] activity

1. In [!DNL Target], navigieren Sie zum **[!UICONTROL Tätigkeiten]** Seite und wählen Sie **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

   ![ALT-Bild](assets/asset-ab.png)

1. Im **[!UICONTROL A/B-Test-Aktivität erstellen]** modal, lassen Sie die Standardoption Web ausgewählt (1), wählen Sie **[!UICONTROL Formular]** Wählen Sie als Experience Composer (2) **[!UICONTROL Standardarbeitsbereich]** mit **[!UICONTROL Keine Eigenschaftenbeschränkungen]**(3) und klicken Sie auf **[!UICONTROL Nächste]** 4.

   ![ALT-Bild](assets/asset-form.png)

1. Im **[!UICONTROL Erlebnisse]** Schritt der Aktivitätserstellung einen Namen für Ihre Aktivität angeben (1) und ein zweites Erlebnis, Erlebnis B, hinzufügen, indem Sie auf **[!UICONTROL Erlebnis hinzufügen]** Absatz 2. Geben Sie den Ortsnamen Ihrer Wahl ein (3). Beispiel: `ondevice-featureflag` oder `homepage-addtocart-featureflag` sind Ortsnamen, die die Ziele für Feature Flag-Tests angeben.  Im folgenden Beispiel: `ondevice-featureflag` ist der für Erlebnis B definierte Ort. Optional können Sie Zielgruppenverfeinerungen (4) hinzufügen, um die Qualifizierung auf die Aktivität zu beschränken.

   ![ALT-Bild](assets/asset-location.png)

1. Im **[!UICONTROL Inhalt]** auf derselben Seite ein und wählen Sie **[!UICONTROL JSON-Angebot erstellen]** in der Dropdown-Liste (1) angezeigt.

   ![ALT-Bild](assets/asset-offer.png)

1. Im **[!UICONTROL JSON-Daten]** in das Textfeld ein, geben Sie Ihre Funktionsmarkierungsvariablen für jedes Erlebnis (1) ein und verwenden Sie ein gültiges JSON-Objekt (2).

   Geben Sie die Variablen für die Funktionskennzeichnung für Erlebnis A ein.

   ![ALT-Bild](assets/asset-json_a.png)

   **(Beispiel-JSON für Erlebnis A oben)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expA"
   }
   ```

   Geben Sie die Variablen für das Feature Flag für Erlebnis B ein.

   ![ALT-Bild](assets/asset-json_b.png)

   **(Beispiel-JSON für Erlebnis B oben)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expB"
   }
   ```

1. Klicks **[!UICONTROL Nächste]** 1. **[!UICONTROL Targeting]** Schritt der Aktivitätserstellung.

   ![ALT-Bild](assets/asset-next_2_t.png)

1. Im **[!UICONTROL Targeting]** Beispiel für einen Schritt unten gezeigt, bleibt das Zielgruppen-Targeting (2) aus Gründen der Einfachheit im Standardsatz Alle Besucher enthalten. Dies bedeutet, dass die Aktivität nicht zielgerichtet ist. Beachten Sie jedoch, dass Sie in der Adobe immer Zielgruppen für Produktionsaktivitäten auswählen sollten. Klicks **[!UICONTROL Nächste]** 3. **[!UICONTROL Ziele und Einstellungen]** Schritt der Aktivitätserstellung.

   ![ALT-Bild](assets/asset-next_2_g.png)

1. Im **[!UICONTROL Ziele und Einstellungen]** Schritt, festlegen **[!UICONTROL Berichtsquelle]** nach **[!UICONTROL Adobe Target]** Absatz 1. Definieren Sie die **[!UICONTROL Zielmetrik]** as **[!UICONTROL Konversion]**, wobei die Details auf Grundlage der Konversionsmetriken Ihrer Site (2) angegeben werden. Klicks **[!UICONTROL Speichern und schließen]** (3) , um die Aktivität zu speichern.

   ![ALT-Bild](assets/asset-conv.png)

## 5. Implementieren und Rendern der Funktion in Ihrer Anwendung

Nach dem Einrichten der Feature Flag-Variablen in [!DNL Target]ändern Sie den Anwendungs-Code, um ihn zu verwenden. Nachdem Sie beispielsweise das Feature Flag in der Anwendung erhalten haben, können Sie damit Funktionen aktivieren und das Erlebnis rendern, für das sich der Besucher qualifiziert hat.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
let featureFlags = {};
​
function targetClientReady() {
   tClient.getAttributes(["ondevice-featureflag"]).then(function(response) {
      const featureFlags = response.asObject("ondevice-featureflag");
      if(featureFlags.enabled && featureFlags.flag !== "expA") { //Assuming "expA" is control
         console.log("Render alternate experience" + featureFlags.flag);
      }
      else {
         console.log("Render default experience");
      }
   });
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("ondevice-featureflag").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
   .context(new Context().channel(ChannelType.WEB))
   .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
   .build();
Attributes attributes = targetClient.getAttributes(request, "ondevice-featureflag");
String flag = attributes.getString("ondevice-featureflag", "flag");
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var mbox = new MboxRequest(index: 0, name: "ondevice-featureflag");
var deliveryRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { mbox }))
   .Build();
var attributes = targetClient.GetAttributes(request, "ondevice-featureflag");
var flag = attributes.GetString("ondevice-featureflag", "flag");
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

feature_flags = {}

def target_client_ready():
   attribute_provider = target_client.get_attributes(["ondevice-featureflag"])
   feature_flags = attribute_provider.as_object(mbox_name="ondevice-featureflag")
   if feature_flags.get("enabled") and feature_flags.get("flag") != "expA": # Assuming "expA" is control
      print("Render alternate experience {}".format(feature_flags.get("flag")))
   else:
      print("Render default experience")
```

>[!ENDTABS]

## 6. Implementieren Sie zusätzliches Tracking für Ereignisse in Ihrer Anwendung

Optional können Sie mithilfe der Funktion sendNotification() zusätzliche Ereignisse zum Verfolgen von Konversionen senden.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
//When a conversion happens
TargetClient.sendNotifications({
   targetCookie,
   "request" : {
      "notifications" : [
      {
         type: "display",
         timestamp : Date.now(),
         id: "conversion",
         mbox : {
            name : "orderConfirm"
         },
         order : {
            id: "BR9389",
            total : 98.93,
            purchasedProductIds : ["J9393", "3DJJ3"]
         }
      }
      ]
   }
})
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.DISPLAY);
notification.setTimestamp(System.currentTimeMillis());
Order order = new Order("BR9389");
order.total(98.93);
order.purchasedProductIds(["J9393", "3DJJ3"]);
notification.setOrder(order);

TargetDeliveryRequest notificationRequest =
   TargetDeliveryRequest.builder()
      .context(new Context().channel(ChannelType.WEB))
      .notifications(Collections.singletonList(notification))
      .build();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();
notificationDeliveryService.sendNotification(notificationRequest);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var order = new Order
{
   Id = "BR9389",
   Total = 98.93M,
   PurchasedProductIds = new List<string> { "J9393", "3DJJ3" },
};
​
var notification = new Notification
{
   Id = "conversion",
   ImpressionId = Guid.NewGuid().ToString(),
   Type = MetricType.Display,
   Timestamp = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
   Order = order,
};
​
var notificationRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetNotifications(new List<Notification> {notification})
   .Build();
​
targetClient.SendNotifications(notificationRequest);
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

# When a conversion happens
notification_mbox = NotificationMbox(name="orderConfirm")
order = Order(id="BR9389, total=98.93, purchased_product_ids=["J9393", "3DJJ3"])
notification = Notification(
   id="conversion",
   type=MetricType.DISPLAY,
   timestamp=1621530726000,  # Epoch time in milliseconds
   mbox=notification_mbox,
   order=order
)
notification_request = DeliveryRequest(notifications=[notification])


target_client.send_notifications({
   "target_cookie": target_cookie,
   "request" : notification_request
})
```

>[!ENDTABS]

## 7. Aktivieren Sie Ihre [!UICONTROL A/B-Test] activity

1. Klicks **[!UICONTROL Aktivieren]** (1) zur Aktivierung Ihrer [!UICONTROL A/B-Test] -Aktivität.

   >[!NOTE]
   >
   >Sie müssen über die **[!UICONTROL Genehmiger]** oder **[!UICONTROL Herausgeber]** [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um diesen Schritt durchzuführen.

   ![ALT-Bild](assets/asset-activate.png)
