---
title: Erste Schritte mit Target-SDKs
description: Wie verwende ich die Adobe Target SDKs?
feature: APIs/SDKs
exl-id: a5ae9826-7bb5-41de-8796-76edc4f5b281
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Erste Schritte mit [!DNL Target] SDKs

Um die Arbeit zu starten, empfehlen wir, die erste Feature Flag-Aktivität [on-device decisioning](../on-device-decisioning/overview.md) in der Sprache Ihrer Wahl zu erstellen:

* Node.js
* Java
* .NET
* Python

## Zusammenfassung der Schritte

1. Aktivieren der geräteübergreifenden Entscheidungsfindung für Ihre Organisation
1. SDK installieren
1. Initialisieren des SDK
1. Einrichten der Funktionsmarkierungen in einer [!DNL Adobe Target] [!UICONTROL A/B Test] -Aktivität
1. Funktion in Ihre Anwendung implementieren und rendern
1. Implementieren des Trackings für Ereignisse in Ihrer Anwendung
1. Aktivieren Ihrer [!UICONTROL A/B Test] -Aktivität

## 1. Aktivieren Sie die Entscheidungsfindung auf dem Gerät für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine [!UICONTROL A/B Test] -Aktivität mit nahezu Nulllatenz ausgeführt wird. Um diese Funktion zu aktivieren, navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

![alt image](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über die Benutzerrolle **[!UICONTROL Admin]** oder **[!UICONTROL Approver]** [3} verfügen, um den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren oder zu deaktivieren.](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html)

Nachdem Sie den Umschalter **[!UICONTROL On-Device Decisioning]** aktiviert haben, beginnt [!DNL Adobe Target] mit der Generierung von [Regel-Artefakten](../on-device-decisioning/rule-artifact-overview.md) für Ihren Client.

## 2. Installieren des SDK

Führen Sie für Node.js, Java und Python den folgenden Befehl in Ihrem Projektverzeichnis im Terminal aus. Fügen Sie .NET als Abhängigkeit von [aus NuGet](https://www.nuget.org/packages/Adobe.Target.Client) installieren.

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

>[!TAB node.js]

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

## 4. Einrichten der Funktionsmarkierungen in einer [!DNL Adobe Target] [!UICONTROL A/B Test] -Aktivität

1. Navigieren Sie in [!DNL Target] zur Seite **[!UICONTROL Activities]** und wählen Sie dann **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]** aus.

   ![alt image](assets/asset-ab.png)

1. Lassen Sie im Modal **[!UICONTROL Create A/B Test Activity]** die standardmäßige Web-Option ausgewählt (1), wählen Sie **[!UICONTROL Form]** als Ihren Experience Composer (2), wählen Sie **[!UICONTROL Default Workspace]** mit **[!UICONTROL No Property Restrictions]**(3) und klicken Sie dann auf **[!UICONTROL Next]** (4).

   ![alt image](assets/asset-form.png)

1. Geben Sie im Schritt **[!UICONTROL Experiences]** der Aktivitätserstellung einen Namen für Ihre Aktivität (1) ein und fügen Sie ein zweites Erlebnis, Erlebnis B, hinzu, indem Sie auf **[!UICONTROL Add Experience]** (2) klicken. Geben Sie den Ortsnamen Ihrer Wahl ein (3). Beispielsweise sind `ondevice-featureflag` oder `homepage-addtocart-featureflag` Standortnamen, die die Ziele für Feature Flag-Tests angeben.  Im folgenden Beispiel ist `ondevice-featureflag` der für Erlebnis B definierte Ort. Optional können Sie Zielgruppenverfeinerungen (4) hinzufügen, um die Qualifizierung auf die Aktivität zu beschränken.

   ![alt image](assets/asset-location.png)

1. Wählen Sie im Abschnitt **[!UICONTROL CONTENT]** auf derselben Seite **[!UICONTROL Create JSON Offer]** in der Dropdown-Liste (1) aus, wie unten dargestellt.

   ![alt image](assets/asset-offer.png)

1. Geben Sie im angezeigten Textfeld **[!UICONTROL JSON Data]** Ihre Variablen für die Feature Flag für jedes Erlebnis (1) ein, indem Sie ein gültiges JSON-Objekt (2) verwenden.

   Geben Sie die Variablen für die Funktionskennzeichnung für Erlebnis A ein.

   ![alt image](assets/asset-json_a.png)

   **(Beispiel-JSON für Erlebnis A, oben)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expA"
   }
   ```

   Geben Sie die Variablen für das Feature Flag für Erlebnis B ein.

   ![alt image](assets/asset-json_b.png)

   **(Beispiel-JSON für Erlebnis B, oben)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expB"
   }
   ```

1. Klicken Sie auf **[!UICONTROL Next]** (1) , um zum Schritt **[!UICONTROL Targeting]** der Aktivitätserstellung zu gelangen.

   ![alt image](assets/asset-next_2_t.png)

1. Im unten gezeigten Beispiel **[!UICONTROL Targeting]**-Schrittbeispiel bleibt Zielgruppen-Targeting (2) aus Gründen der Einfachheit im Standardsatz Alle Besucher enthalten. Dies bedeutet, dass die Aktivität nicht zielgerichtet ist. Beachten Sie jedoch die Adobe, dass Sie immer Ihre Zielgruppen für Produktionsaktivitäten auswählen. Klicken Sie auf **[!UICONTROL Next]** (3) , um zum Schritt **[!UICONTROL Goals & Settings]** der Aktivitätserstellung zu gelangen.

   ![alt image](assets/asset-next_2_g.png)

1. Setzen Sie im Schritt **[!UICONTROL Goals & Settings]** **[!UICONTROL Reporting Source]** auf **[!UICONTROL Adobe Target]** (1). Definieren Sie den **[!UICONTROL Goal Metric]** als **[!UICONTROL Conversion]** und geben Sie die Details basierend auf den Konversionsmetriken Ihrer Site an (2). Klicken Sie auf **[!UICONTROL Save & Close]** (3) , um die Aktivität zu speichern.

   ![alt image](assets/asset-conv.png)

## 5. Implementieren und Rendern der Funktion in Ihrer Anwendung

Nachdem Sie die Variablen für die Feature Flag in [!DNL Target] eingerichtet haben, ändern Sie Ihren Anwendungscode so, dass er sie verwendet. Nachdem Sie beispielsweise das Feature Flag in der Anwendung erhalten haben, können Sie damit Funktionen aktivieren und das Erlebnis rendern, für das sich der Besucher qualifiziert hat.

>[!BEGINTABS]

>[!TAB node.js]

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

>[!TAB node.js]

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

## 7. Aktivieren Sie Ihre [!UICONTROL A/B Test] -Aktivität

1. Klicken Sie auf **[!UICONTROL Activate]** (1) , um Ihre [!UICONTROL A/B Test] -Aktivität zu aktivieren.

   >[!NOTE]
   >
   >Sie müssen über die Benutzerrolle **[!UICONTROL Approver]** oder **[!UICONTROL Publisher]** [3} verfügen, um diesen Schritt durchzuführen.](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html)

   ![alt image](assets/asset-activate.png)
