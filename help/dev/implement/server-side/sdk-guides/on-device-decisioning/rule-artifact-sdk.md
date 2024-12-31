---
title: Automatisches Herunterladen, Speichern und Aktualisieren des Artefakts der geräteinternen Entscheidungsregel
description: Erfahren Sie, wie Sie beim Initialisieren der  [!DNL Adobe Target] SDK mit dem Artefakt „Entscheidungsregel auf dem Gerät“ arbeiten.
feature: APIs/SDKs
exl-id: be41a723-616f-4aa3-9a38-8143438bd18a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Automatisches Herunterladen, Speichern und Aktualisieren des Regelartefakts über die [!DNL Adobe Target] SDK

Dieser Ansatz eignet sich am besten, wenn Sie die [!DNL Adobe Target] SDK initialisieren können, während Sie gleichzeitig Ihren Webserver initialisieren und starten. Das Regelartefakt wird von der [!DNL Adobe Target] SDK heruntergeladen und im Arbeitsspeicher zwischengespeichert, bevor die Webserveranwendung mit der Bereitstellung von Anfragen beginnt. Sobald Ihre Web-Anwendung ausgeführt wird, werden alle [!DNL Adobe Target] Entscheidungen mit dem In-Memory-Regel-Artefakt ausgeführt. Das zwischengespeicherte Regelartefakt wird basierend auf dem `pollingInterval` aktualisiert, den Sie beim SDK-Initialisierungsschritt angeben.

## Zusammenfassung der Schritte

1. Installieren von SDK
1. SDK initialisieren
1. Speichern und Verwenden des Regelartefakts

## 1. Installieren des SDKS

>[!BEGINTABS]

>[!TAB NPM]

```javascript {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB MVN]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
</dependency>
```

>[!ENDTABS]

## 2. SDK initialisieren

1. Importieren Sie zunächst die SDK. Importieren Sie in dieselbe Datei, von der aus Sie den Serverstart steuern können.

   **Node.js**

   ```javascript {line-numbers="true"}
   const TargetClient = require("@adobe/target-nodejs-sdk");
   ```

   **Java**

   ```javascript {line-numbers="true"}
   import com.adobe.target.edge.client.ClientConfig;
   import com.adobe.target.edge.client.TargetClient;
   ```

1. Verwenden Sie zum Konfigurieren der SDK die Create-Methode.

   **Node.js**

   ```javascript {line-numbers="true"}
   const CONFIG = {
       client: "<your target client code>",
       organizationId: "your EC org id",
       decisioningMethod: "on-device",
       pollingInterval : 300000,
       events: {
           clientReady: startWebServer
       }
   };
   
   const TargetClient = TargetClient.create(CONFIG);
   
   function startWebServer() {
       //Adobe Target SDK has now downloaded the JSON Artifacts and is available in the memory.
       //You can start your web server now to serve requests now.
   }
   ```

   **Java**

   ```javascript {line-numbers="true"}
   ClientConfig config = ClientConfig.builder()
       .client("<you target client code>")
       .organizationId("<your EC org id>")
       .build();
   TargetClient targetClient = TargetClient.create(config);
   ```

1. Sowohl die Client- als auch die Organisations-ID können aus [!DNL Adobe Target] abgerufen werden, indem Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** navigieren, wie hier dargestellt.

   &lt;!— insert image-client-code.png —>
   ![Implementierungsseite unter „Administration“ in Target](assets/asset-rule-artifact-3.png)

## 3. Speichern und verwenden Sie das Regelartefakt

Sie müssen das Regelartefakt nicht selbst verwalten, und der Aufruf der SDK-Methoden sollte unkompliziert sein.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
//req is the request object from the server request listener method
const targetCookie = req.cookies[TargetClient.TargetCookieName];
const request = {
    context: {
        channel: "web"
    },
    execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner"
        }],
    },
};

TargetClient.getOffers({
    request,
    targetCookie
}).then(function(response) {
    //This Target response is coming from the In-memory Target artifact.
    console.log("Target response", response);
}).catch(function(err) {
    console.error("Target:", err);
})
```

>[!TAB Java]

```java {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

>[!NOTE]
>
>Im obigen Codebeispiel enthält das `TargetClient`-Objekt einen Verweis auf das speicherinterne Regelartefakt. Wenn Sie dieses Objekt zum Aufrufen von SDK-Standardmethoden verwenden, verwendet es das speicherinterne Regelartefakt für die Entscheidungsfindung. Wenn Ihre Anwendung so strukturiert ist, dass Sie die SDK-Methoden in anderen Dateien als derjenigen aufrufen müssen, die Client-Anfragen initialisiert und abhört, und wenn diese Dateien keinen Zugriff auf das TargetClient-Objekt haben, können Sie die JSON-Payload herunterladen und in einer lokalen JSON-Datei speichern, die für andere Dateien verwendet werden soll, die die SDK initialisieren müssen. Dies wird im nächsten Abschnitt bezüglich des [Herunterladens des Regelartefakts mithilfe einer JSON-Payload) ](rule-artifact-json.md).

Im Folgenden finden Sie ein Beispiel, das eine Web-Anwendung nach der Initialisierung der [!DNL Adobe Target] SDK startet.

>[!BEGINTABS]

>[!TAB Node.js]

```javascript {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
    client: "<your target client code>",
    organizationId: "your EC org id",
    decisioningMethod: "on-device",
    pollingInterval : 300000,
    events: {
        clientReady: startWebServer
    }
};

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());
  saveCookie(res, response.targetCookie);
  res.status(200).send(response);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

function startWebServer() {
    app.get('/*', async (req, res) => {
    const targetCookie = req.cookies[TargetClient.TargetCookieName];
    const request = {
        execute: {
        mboxes: [{
            address: { url: req.headers.host + req.originalUrl },
            name: "on-device-homepage-banner" // Ensure that you have a LIVE Activity running on this location
        }]
        }};

    try {
        const response = await targetClient.getOffers({ request, targetCookie });
        sendSuccessResponse(res, response);
    } catch (error) {
        console.error("Target:", error);
        sendErrorResponse(res, error);
    }
    });

    app.listen(3000, function () {
    console.log("Listening on port 3000 and watching!");
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

@Controller
public class TargetController {

  private TargetClient targetClient;

  TargetController() {
    // You should instantiate TargetClient in a Bean and inject the instance into this class 
    // but we show the code here for demonstration purpose.
    ClientConfig config = ClientConfig.builder()
        .client("<you target client code>")
        .organizationId("<your EC org id>")
        .build();
    targetClient = TargetClient.create(config);
  }

  @GetMapping("/")
  public String homePage() {
    MboxRequest mbox = new MboxRequest().name("homepage").index(0);
    TargetDeliveryRequest request = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
        .build();
    TargetDeliveryResponse response = targetClient.getOffers(request);
    // ...
  }
}
```

>[!ENDTABS]
