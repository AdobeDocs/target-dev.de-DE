---
title: Integration mit Experience Cloud AAM Segmenten
description: Integration mit Experience Cloud, Audience Manager-Integration
keywords: Bereitstellungs-API, Server-seitig, serverseitig, Integration, Audience Manager, AAM
exl-id: c21e0200-23ba-4a0b-adf4-38e03c087f00
feature: Implement Server-side
source-git-commit: e3f14e97fa48ffb1f07b29aca5711d16e75faa80
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---

# AAM-Segmente

[!DNL Adobe Audience Manager] -Segmente können über [!DNL Adobe Target] SDKs Um AAM Segmente nutzen zu können, müssen die folgenden Felder angegeben werden:

>[!NOTE]
>
>AAM Segmente werden für Entscheidungsaktivitäten auf dem Gerät nicht unterstützt.

| Feldname | Erforderlich | Beschreibung |
| --- | --- | --- |
| `locationHint` | Ja | DCS-Standorthinweis wird verwendet, um zu bestimmen, welcher DCS-Endpunkt getroffen werden AAM, um das Profil abzurufen. Muss >= 1 sein. |
| `marketingCloudVisitorId` | Ja | Marketing Cloud-Besucher-ID |
| `blob` | Ja | AAM Blob wird verwendet, um zusätzliche Daten an AAM zu senden. Darf nicht leer sein und die Größe &lt;= 1024. |

Das SDK füllt diese Felder automatisch für Sie aus, wenn Sie eine `getOffers` -Methodenaufruf, Sie müssen jedoch sicherstellen, dass ein gültiges Besucher-Cookie bereitgestellt wird. Um dieses Cookie zu erhalten, müssen Sie VisitorAPI.js im Browser implementieren.

## Implementierungshandbuch

### Verwendung von Cookies

Cookies werden zur Korrelation verwendet [!DNL Adobe Audience Manager] Anforderungen mit [!DNL Adobe Target] -Anfragen. Dies sind die Cookies, die in dieser Implementierung verwendet werden.

| Cookie | Name | Beschreibung |
| --- | --- | --- |
| Besucher-Cookie | `AMCVS_XXXXXXXXXXXXXXXXXXXXXXXX%40AdobeOrg` | Dieses Cookie wird von `VisitorAPI.js` wenn es mit initialisiert wird `visitorState` aus der Zielgruppe `getOffers` Antwort. |
| Zielcookie | `mbox` | Ihr Webserver muss dieses Cookie mit dem Namen und Wert von `targetCookie` aus der Zielgruppe `getOffers` Antwort. |

### Übersicht über die Schritte

Angenommen, ein Benutzer gibt eine URL in einen Browser ein, der eine Anforderung an Ihren Webserver sendet. Bei Erfüllung dieser Anforderung:

1. Der Server liest die Besucher- und Target-Cookies aus der Anforderung.
1. Der Server ruft die `getOffers` -Methode [!DNL Target] SDK, wobei die Besucher- und Target-Cookies angegeben werden, sofern verfügbar.
1. Wenn die Variable `getOffers` -Aufruf erfüllt ist, Werte für `targetCookie` und `visitorState` aus der Antwort verwendet werden.
   1. Ein Cookie wird in der Antwort gesetzt, wobei die Werte aus `targetCookie`. Dies geschieht mithilfe der `Set-Cookie` Antwortheader, der den Browser anweist, das Ziel-Cookie zu behalten.
   1. Es wird eine HTML-Antwort vorbereitet, die initialisiert wird. `VisitorAPI.js` und übergeben `visitorState` aus der Zielantwort.
1. Die HTML-Antwort wird im Browser geladen...
   1. `VisitorAPI.js` ist in der Kopfzeile des Dokuments enthalten.
   1. VisitorAPI wird mit `visitorState` aus dem `getOffers` SDK-Antwort. Dadurch wird das Besucher-Cookie im Browser gesetzt, sodass es bei nachfolgenden Anfragen an den Server gesendet wird.

### Beispielcode

Im folgenden Codebeispiel werden die oben beschriebenen Schritte implementiert. Jeder Schritt wird im Code als Inline-Kommentar neben der Implementierung angezeigt.

#### Node.js

Dieses Beispiel beruht auf [Express, ein Node.js-Web-Framework](https://expressjs.com/).

>[!BEGINTABS]

>[!TAB server.js]

```js {line-numbers="true"}
const fs = require("fs");
const express = require("express");
const cookieParser = require("cookie-parser");
const Handlebars = require("handlebars");
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  timeout: 10000,
  logger: console,
};
const targetClient = TargetClient.create(CONFIG);
const TEMPLATE = fs.readFileSync(`${__dirname}/index.handlebars`).toString();
const handlebarsTemplate = Handlebars.compile(TEMPLATE);

Handlebars.registerHelper("toJSON", function (object) {
  return new Handlebars.SafeString(JSON.stringify(object, null, 4));
});

const app = express();
app.use(cookieParser());
app.use(express.static(__dirname + "/public"));

app.get("/", async (req, res) => {
  // The server reads the visitor and target cookies from the request.
  const visitorCookie =
    req.cookies[
      encodeURIComponent(
        TargetClient.getVisitorCookieName(CONFIG.organizationId)
      )
    ];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const address = { url: req.headers.host + req.originalUrl };

  const targetRequest = {
    execute: {
      mboxes: [
        { name: "homepage", index: 1, address },
        { name: "SummerShoesOffer", index: 2, address },
        { name: "SummerDressOffer", index: 3, address }
      ],
    },
  };

  res.set({
    "Content-Type": "text/html",
    Expires: new Date().toUTCString(),
  });

  try {
    // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
    const targetResponse = await targetClient.getOffers({
      request: targetRequest,
      visitorCookie,
      targetCookie,
    });

    // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
    // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
    res.cookie(
      targetResponse.targetCookie.name,
      targetResponse.targetCookie.value,
      { maxAge: targetResponse.targetCookie.maxAge * 1000 }
    );

    // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
    const html = handlebarsTemplate({
      organizationId: CONFIG.organizationId,
      targetResponse,
    });

    res.status(200).send(html);
  } catch (error) {
    console.error("Target:", error);
    res.status(500).send(error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB index.handlebars]

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>

  <!-- VisitorAPI.js is included in the document header. -->
  <script src="VisitorAPI.js"></script>
  <script>
    // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
    Visitor.getInstance("{{organizationId}}", {serverState: {{toJSON targetResponse.visitorState}} });
  </script>
</head>
<body>
  <h1>response</h1>
  <pre>{{toJSON targetResponse}}</pre>
</body>
</html>
```

>[!ENDTABS]

#### Java

Dieses Beispiel verwendet [Frühjahr, ein Java-Web-Framework](https://spring.io/).

>[!BEGINTABS]

>[!TAB ClientSampleApplication.java]

```java {line-numbers="true"}
@SpringBootApplication
public class ClientSampleApplication {

    public static void main(String[] args) {
        System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
        SpringApplication.run(ClientSampleApplication.class, args);
    }

    @Bean
    TargetClient marketingCloudClient() {
        ClientConfig clientConfig = ClientConfig.builder()
                .client("acmeclient")
                .organizationId("1234567890@AdobeOrg")
                .defaultDecisioningMethod(DecisioningMethod.SERVER_SIDE)
                .build();

        return TargetClient.create(clientConfig);
    }
}
```

>[!TAB TargetController.java]

```java {line-numbers="true"}
@Controller
@RequestMapping("/")
public class TargetController {

    @Autowired
    private TargetClientService targetClientService;

    @GetMapping
    public String index(Model model, HttpServletRequest request, HttpServletResponse response) {
        // The server reads the visitor and target cookies from the request.
        List<TargetCookie> targetCookies = getTargetCookies(request.getCookies());

        Address address = getAddress(request);

        List<MboxRequest> mboxRequests = new ArrayList<>();
        mboxRequests.add((MboxRequest) new MboxRequest().name("homepage").index(1).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerShoesOffer").index(2).address(address));
        mboxRequests.add((MboxRequest) new MboxRequest().name("SummerDressOffer").index(3).address(address));

        TargetDeliveryResponse targetDeliveryResponse = targetClientService.getOffers(mboxRequests, targetCookies, request,
                response);

        // An HTML response is prepared that initializes VisitorAPI.js and passes in `visitorState` from the target response.
        model.addAttribute("visitorState", targetDeliveryResponse.getVisitorState());
        model.addAttribute("targetResponse", targetDeliveryResponse);
        model.addAttribute("organizationId", "1234567890@AdobeOrg");

        return "index";
    }
}
```

>[!TAB TargetClientService.java]

```java {line-numbers="true"}
@Service
public class TargetClientService {

    private final TargetClient targetJavaClient;

    public TargetClientService(TargetClient targetJavaClient) {
        this.targetJavaClient = targetJavaClient;
    }

    public TargetDeliveryResponse getOffers(List<MboxRequest> executeMboxes, List<TargetCookie> cookies, HttpServletRequest request, HttpServletResponse response) {

        Context context = getContext(request);
        ExecuteRequest executeRequest = new ExecuteRequest();
        executeRequest.setMboxes(executeMboxes);

        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .execute(executeRequest)
                .cookies(cookies)
                .build();

        // The server makes a call to the `getOffers` method of the Target SDK specifying the visitor and target cookies if available.
        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);

        // When the `getOffers` call is fulfilled, values for `targetCookie` and `visitorState` from the response are used.
        // A cookie is set on the response with values taken from `targetCookie`.  This is done using the `Set-Cookie` response header which tells the browser to persist the target cookie.
        setCookies(targetResponse.getCookies(), response);
        return targetResponse;
    }
}
```

>[!TAB TargetRequestUtils.java]

```java {line-numbers="true"}
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Target Only : GetOffer</title>

    <!-- VisitorAPI.js is included in the document header. -->
    <script src="../../js/VisitorAPI.js"></script>
    <script th:inline="javascript">
        // VisitorAPI is initialized with visitorState from the `getOffers` SDK response. This will cause the visitor cookie to be set in the browser so it will be sent to the server on subsequent requests.
        Visitor.getInstance(/*[[${organizationId}]]*/ "", {serverState: /*[[${visitorState}]]*/ {}});
    </script>
</head>
<body>
    <h1>response</h1>
    <pre>[[${targetResponse}]]</pre>
</body>
</html>
```

>[!ENDTABS]

Weitere Informationen finden Sie unter `TargetRequestUtils.java`, siehe [Dienstprogrammmethoden (Java)](https://experienceleague.adobe.com/docs/target-dev/developer/server-side/java/utility-methods.html){target=_blank}
