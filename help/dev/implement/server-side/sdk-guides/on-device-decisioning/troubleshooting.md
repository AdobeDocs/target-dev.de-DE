---
title: Fehlerbehebung bei geräteübergreifenden Entscheidungen
description: Erfahren Sie, wie Sie die Fehlerbehebung für [!UICONTROL on-device decisioning] durchführen.
exl-id: e76f95ce-afae-48e0-9dbb-2097133574dc
feature: APIs/SDKs
source-git-commit: 1d892d4d4d6f370f7772d0308ee0dd0d5c12e700
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Fehlerbehebung [!UICONTROL on-device decisioning]

## Validieren der Konfiguration

### Zusammenfassung der Schritte

1. Stellen Sie sicher, dass `logger` konfiguriert ist.
1. Stellen Sie sicher, dass [!DNL Target] Traces aktiviert ist.
1. Stellen Sie sicher, dass das [!UICONTROL on-device decisioning] *Regel-Artefakt* abgerufen und gemäß dem definierten Abrufintervall zwischengespeichert wurde.
1. Validieren Sie die Inhaltsbereitstellung über das zwischengespeicherte Regel-Artefakt, indem Sie eine Test- [!UICONTROL on-device decisioning] -Aktivität über den formularbasierten Experience Composer erstellen.
1. Inspect sendet Benachrichtigungsfehler

## 1. Stellen Sie sicher, dass der Logger konfiguriert ist.

Stellen Sie beim Initialisieren des SDK sicher, dass Sie die Protokollierung aktivieren.

**node.js**

Für das Node.js-SDK sollte ein `logger` -Objekt bereitgestellt werden.

```js {line-numbers="true"}
const CONFIG = {
  client: "<your client code>",
  organizationId: "<your organization ID>",
  logger: console
};
```

**Java-SDK**

Für Java-SDK `logRequests` sollte die `ClientConfig` aktiviert sein.

```js {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("<your client code>")
  .organizationId("<your organization ID>")
  .logRequests(true)
  .build();
```

Außerdem sollte die JVM mit dem folgenden Befehlszeilenparameter gestartet werden:

```bash {line-numbers="true"}
java -Dorg.slf4j.simpleLogger.defaultLogLevel=DEBUG ...
```

## 2. Stellen Sie sicher, dass [!DNL Target]Traces aktiviert ist.

Durch das Aktivieren von Traces werden zusätzliche Informationen von [!DNL Adobe Target] in Bezug auf das Regelartefakt ausgegeben.

1. Navigieren Sie in [!DNL Experience Cloud] zur UI[!DNL Target].

   ![alt image](assets/asset-target-ui-1.png)

1. Navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** und klicken Sie auf **[!UICONTROL Generate New Authorization Token]**.

   ![alt image](assets/asset-target-ui-2.png)

1. Kopieren Sie das neu generierte Autorisierungstoken in die Zwischenablage und fügen Sie es zu Ihrer[!DNL Target]Anfrage hinzu:

   **node.js**

   ```js {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: "88f1a924-6bc5-4836-8560-2f9c86aeb36b"
     },
     execute: {
       mboxes: [{
         name: "sdk-mbox"
       }]
   }};
   ```

   **Java**

   ```js {line-numbers="true"}
   Trace trace = new Trace()
     .authorizationToken("88f1a924-6bc5-4836-8560-2f9c86aeb36b");
   Context context = new Context()
     .channel(ChannelType.WEB);
   MboxRequest mbox = new MboxRequest()
     .name("sdk-mbox")
     .index(0);
   ExecuteRequest executeRequest = new ExecuteRequest()
     .mboxes(Arrays.asList(mbox));
   
   TargetDeliveryRequest request = TargetDeliveryRequest.builder()
     .trace(trace)
     .context(context)
     .execute(executeRequest)
     .build();
   ```

1. Starten Sie Ihre App, während Sie die Protokollfunktion eingerichtet haben, und überwachen Sie das Server-Terminal. Die folgende Ausgabe der Protokollfunktion bestätigt, dass das Regelartefakt abgerufen wurde:

   **Node.js-SDK**

   ```text {line-numbers="true"}
     AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-code/production/v1/rules.json
     AT: LD.ArtifactProvider artifact received - status=200
   ```

## 3. Stellen Sie sicher, dass das [!UICONTROL on-device decisioning] *Regel-Artefakt* abgerufen und gemäß dem definierten Abrufintervall zwischengespeichert wurde.

1. Warten Sie die Dauer des Abrufintervalls (standardmäßig 20 Minuten) und stellen Sie sicher, dass das Artefakt vom SDK abgerufen wird. Es werden dieselben Terminalprotokolle ausgegeben.

   Darüber hinaus sollten Informationen aus der[!DNL Target]Ablaufverfolgung mit Details zum Regelartefakt an das Terminal ausgegeben werden.

   ```text {line-numbers="true"}
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
       "clientCode": "your-client-code",
       "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```

## 4. Validieren Sie die Inhaltsbereitstellung über das zwischengespeicherte Regel-Artefakt, indem Sie eine Test [!UICONTROL on-device decisioning] -Aktivität über den formularbasierten Experience Composer erstellen

1. Navigieren Sie zur[!DNL Target]UI im Experience Cloud.

   ![alt image](assets/asset-target-ui-1.png)

1. Erstellen Sie mit dem formularbasierten Experience Composer eine neue XT-Aktivität.

   ![alt image](assets/asset-form-base-composer-ui.png)

1. Geben Sie den in Ihrer[!DNL Target]Anfrage verwendeten Mbox-Namen als Speicherort für die XT-Aktivität ein (beachten Sie, dass dies ein eindeutiger Mbox-Name sein sollte, der speziell für Entwicklungszwecke verwendet wird).

   ![alt image](assets/asset-mbox-location-ui.png)

1. Ändern Sie den Inhalt in ein HTML- oder JSON-Angebot. Dies wird in der [!DNL Target]Anfrage an Ihre Anwendung zurückgegeben. Belassen Sie das Targeting für die Aktivität auf &quot;Alle Besucher&quot;und wählen Sie eine beliebige Metrik aus. Benennen Sie die Aktivität, speichern Sie sie und aktivieren Sie sie, um sicherzustellen, dass die verwendete Mbox/Position nur für die Entwicklung verwendet wird.

   ![alt image](assets/asset-target-content-ui.png)

1. Fügen Sie in Ihrer Anwendung Protokollanweisungen für den Inhalt hinzu, der in der Antwort von Ihrer[!DNL Target]Anfrage empfangen wurde

   **Node.js-SDK**

   ```js {line-numbers="true"}
   try {
     const response = await targetClient.getOffers({ request });
     console.log('Response: ', response.response.execute.mboxes[0].options[0].content);
   } catch (error) {
     console.error('Something went wrong', error);
   }
   ```

   **Java-SDK**

   ```js {line-numbers="true"}
   try {
     Context context = new Context()
       .channel(ChannelType.WEB);
     MboxRequest mbox = new MboxRequest()
       .name("sdk-mbox")
       .index(0);
     ExecuteRequest executeRequest = new ExecuteRequest()
       .mboxes(Arrays.asList(mbox));
   
     TargetDeliveryRequest request = TargetDeliveryRequest.builder()
       .context(context)
       .decisioningMethod(DecisioningMethod.ON_DEVICE)
       .execute(executeRequest)
       .build();
   
       TargetDeliveryResponse response = targetClient.getOffers(request);
     logger.debug("Response: ", response.getResponse().getExecute().getMboxes().get(0).getOptions().get(0).getContent());
   } catch (Exception exception) {
     logger.error("Something went wrong", exception);
   }
   ```

1. Überprüfen Sie die Protokolle in Ihrem Terminal, um sicherzustellen, dass Ihr Inhalt bereitgestellt und über das Regelartefakt auf Ihrem Server bereitgestellt wird. Das Objekt `LD.DeciscionProvider` wird ausgegeben, wenn die Aktivitätsqualifikation und die Entscheidungsfindung auf dem Gerät basierend auf dem Regelartefakt bestimmt wurden. Darüber hinaus sollte Ihnen aufgrund der Protokollierung von `content` `<div>test</div>` angezeigt werden oder Sie haben sich entschieden, dass die Antwort beim Erstellen der Testaktivität sein soll.

   **Logger output**

   ```text {line-numbers="true"}
   AT: LD.DecisionProvider {...}
   AT: Response received {...}
   Response:  <div>test</div>
   ```

## Inspect sendet Benachrichtigungsfehler

Bei der Verwendung der Entscheidungsfindung auf dem Gerät werden Benachrichtigungen automatisch für die Ausführung von Anfragen durch getOffers gesendet. Diese Anfragen werden still im Hintergrund gesendet. Alle Fehler können durch Abonnieren eines Ereignisses mit dem Namen `sendNotificationError` überprüft werden. Hier finden Sie ein Codebeispiel, das zeigt, wie Sie mit dem Node.js-SDK Benachrichtigungsfehler abonnieren können.

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
let client;

function onSendNotificationError({ notification, error }) {
  console.log(
    `There was an error when sending a notification: ${error.message}`
  );
  console.log(`Notification Payload: ${JSON.stringify(notification, null, 2)}`);
}

async function targetClientReady() {
  const request = {
    context: { channel: "web" },
    execute: {
      mboxes: [{
        name: "a1-serverside-ab",
        index: 1
      }]
    }
  };
  const targetResponse = await client.getOffers({ request });
}

client = TargetClient.create({
  events: {
    clientReady: targetClientReady,
    sendNotificationError: onSendNotificationError
  }
});
```

## Allgemeine Fehlerbehebungsszenarien

Beachten Sie bei Problemen unbedingt die [unterstützten Funktionen](supported-features.md) für [!UICONTROL on-device decisioning] .

### Entscheidungsaktivitäten auf dem Gerät werden aufgrund nicht unterstützter Zielgruppe oder Aktivität nicht ausgeführt

Ein häufiges Problem, das auftreten kann, sind [!UICONTROL on-device decisioning] -Aktivitäten, die aufgrund der verwendeten Zielgruppe oder des nicht unterstützten Aktivitätstyps nicht ausgeführt werden.

(1) Überprüfen Sie mithilfe der Protokollausgabe die Einträge in der Eigenschaft &quot;trace&quot;in Ihrem Antwortobjekt. Ermitteln Sie insbesondere die Kampagneneigenschaft:

**Spurenausgabe**

```text {line-numbers="true"}
  "execute": {
  "mboxes": [
    {
      "name": "your-mbox-name",
      "index": 0,
      "trace": {
        "clientCode": "your-client-code",
        ...
        "campaigns": [],
        ...
      }
    }
```

Sie werden feststellen, dass die Aktivität, für die Sie sich qualifizieren möchten, nicht in der Eigenschaft `campaigns` enthalten ist, da die Zielgruppe oder der Aktivitätstyp nicht unterstützt wird. Wenn die Aktivität unter der Eigenschaft `campaigns` aufgeführt ist, liegt Ihr Problem nicht an einer nicht unterstützten Zielgruppe oder einem nicht unterstützten Aktivitätstyp.

(2) Suchen Sie außerdem die Datei &quot;`rules.json`&quot;, indem Sie in Ihrer Logger-Ausgabe die Datei &quot;`trace` > `artifact` > `artifactLocation`&quot;ansehen und feststellen, dass Ihre Aktivität in der Eigenschaft `rules` > `mboxes` fehlt:

**Logger output**

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: { },
   views: { }
 }
```

Navigieren Sie schließlich zur Benutzeroberfläche[!DNL Target]und suchen Sie die betreffende Aktivität: [experience.adobe.com/target](https://experience.adobe.com/target)

Überprüfen Sie die in der Zielgruppe verwendeten Regeln und stellen Sie sicher, dass Sie nur die oben genannten verwenden, die unterstützt werden. Stellen Sie außerdem sicher, dass der Aktivitätstyp entweder A/B oder XT ist.

![alt image](assets/asset-target-audience-ui.png)

### Entscheidungsaktivitäten auf dem Gerät werden aufgrund einer nicht qualifizierten Zielgruppe nicht ausgeführt

Wenn eine Entscheidungsaktivität auf dem Gerät nicht ausgeführt wird, Sie jedoch überprüft haben, ob die Datei rules.json die Aktivität enthält, führen Sie die folgenden Schritte aus:

(1) Stellen Sie sicher, dass die Mbox, die Sie in Ihrer Anwendung ausführen, mit der von der Aktivität verwendeten übereinstimmt:

>[!BEGINTABS]

>[!TAB rule.json]

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: {
    target-only-node-sdk-mbox: [{ // this mbox name must match the mbox in your request
      ...
    }]
   }
 ...
```

>[!TAB Node.js-SDK]

```js {line-numbers="true"}
 const request = {
   trace: {
     authorizationToken: '2dfc1dce-1e58-4e05-bbd6-a6725893d4d6'
   },
   execute: {
     mboxes: [{
       address: getAddress(req),
       name: "target-only-node-sdk-mbox-two" // this mbox name must match the mbox the activity is using
     }]
   }};
```

>[!TAB Java-SDK]

```js {line-numbers="true"}
Context context = new Context()
  .channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("target-only-node-sdk-mbox-two")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .decisioningMethod(DecisioningMethod.ON_DEVICE)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

(2) Stellen Sie sicher, dass Sie für die Audience für Ihre Aktivität qualifiziert sind, indem Sie die Eigenschaft `matchedRuleConditions` oder `unmatchedRuleConditions` Ihrer Trace-Ausgabe überprüfen:

**Spurenausgabe**

```text {line-numbers="true"}
...
},
"campaignId": 368564,
"campaignType": "landing",
"matchedSegmentIds": [],
"unmatchedSegmentIds": [
  6188838
      ],
      "matchedRuleConditions": [],
          "unmatchedRuleConditions": [
            {
              "in": [
                "true",
                {
                  "var": "mbox.auth_lc"
                }
              ]
            }
          ]
    ...
```

Wenn Sie nicht übereinstimmende Regelbedingungen haben, sind Sie für die Aktivität nicht qualifiziert und die Aktivität wird daher nicht ausgeführt. Überprüfen Sie die Regeln in Ihrer Zielgruppe, um zu sehen, warum Sie sich nicht qualifizieren.

### Die Entscheidungsaktivität auf dem Gerät wird nicht ausgeführt, die Ursache ist jedoch nicht offensichtlich

Es kann nicht leicht erkennbar sein, warum eine Entscheidungsaktivität auf dem Gerät nicht ausgeführt wird. Führen Sie in diesem Fall die folgenden Schritte zur Fehlerbehebung aus, um das Problem zu ermitteln:

(1) Lesen Sie die Protokollverfolgungsausgabe in Ihrer Konsole durch und identifizieren Sie die Artefakteigenschaft, die in etwa wie folgt aussieht:

**Spurenausgabe**

```text {line-numbers="true"}
...
      "artifact": {
          "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
          "pollingInterval": 300000,
          "pollingHalted": false,
          "artifactVersion": "1.0.0",
          "artifactRetrievalCount": 3,
          "artifactLastRetrieved": "2020-10-16T00:56:27.596Z",
          "clientCode": "adobeinterikleisch",
          "environment": "production"
        },
...
```

Sehen Sie sich das Datum `artifactLastRetrieved` des Artefakts an und stellen Sie sicher, dass Sie die neueste `rules.json`-Datei in Ihre App heruntergeladen haben.

(2) Suchen Sie die Eigenschaft `evaluatedCampaignTargets` in Ihrer Protokollausgabe:

**Logger output**

```text {line-numbers="true"}
...
  "evaluatedCampaignTargets": [
      {
        "context": {
          "current_timestamp": 1602812599608,
          "current_time": "0143",
          "current_day": 5,
          "user": {
            "browserType": "unknown",
            "platform": "Unknown",
            "locale": "en",
            "browserVersion": -1
          },
          "page": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "referring": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "geo": {},
          "mbox": {},
          "allocation": 23.79
        },
        "campaignId": 368564,
        "campaignType": "landing",
        "matchedSegmentIds": [],
        "unmatchedSegmentIds": [
          6188838
        ],
        "matchedRuleConditions": [],
        "unmatchedRuleConditions": [
          {
            "in": [
              "true",
              {
                "var": "mbox.auth_lc"
              }
            ]
          }
        ]
...
```

(3) Überprüfen Sie die `context`-, `page`- und `referring`-Daten, um sicherzustellen, dass sie erwartungsgemäß sind, da dies die Zielgruppenqualifizierung der Aktivität beeinflussen kann.

(4) Überprüfen Sie die `campaignId` , um sicherzustellen, dass die Aktivitäten, die Sie erwarten, ausgeführt zu werden, ausgewertet werden. Der `campaignId` entspricht der Aktivitäts-ID auf der Registerkarte &quot;Aktivitätsübersicht&quot;in der [!DNL Target]UI:

![alt image](assets/asset-activity-id-target-ui.png)

(5) Überprüfen Sie die `matchedRuleConditions` und `unmatchedRuleConditions`, um Probleme zu identifizieren, die bei der Qualifizierung für die Zielgruppenregeln für eine bestimmte Aktivität auftreten.

(6) Überprüfen Sie die neueste `rules.json` -Datei, um sicherzustellen, dass die Aktivitäten, die Sie lokal ausführen möchten, eingeschlossen sind. Der Speicherort wird oben in Schritt 1 referenziert.

(7) Stellen Sie sicher, dass Sie in Ihrer Anforderung und in Ihren Aktivitäten dieselben Mbox-Namen verwenden.

(8) Stellen Sie sicher, dass Sie unterstützte Zielgruppenregeln und unterstützte Aktivitätstypen verwenden.

### Ein Server-Aufruf erfolgt, obwohl in der Aktivitäts-Einrichtung unter einer Mbox in der Benutzeroberfläche von [!DNL Target]die Meldung &quot;On Device Decisioning Eligible&quot;angezeigt wird.

Es gibt einige Gründe, warum ein Server-Aufruf erfolgt, obwohl das Gerät für eine geräteübergreifende Entscheidungsfindung qualifiziert ist:

* Wenn die Mbox, die für die Aktivität &quot;Zu Geräteentscheidungen berechtigt&quot;verwendet wird, auch für andere Aktivitäten verwendet wird, die nicht &quot;Zu Geräteentscheidungen berechtigt&quot;sind, wird die Mbox im Abschnitt `remoteMboxes` des Artefakts `rules.json` aufgelistet. Wenn eine Mbox unter `remoteMboxes` aufgeführt wird, führen alle `getOffer(s)` -Aufrufe an diese Mbox zu einem Server-Aufruf.

* Wenn Sie eine Aktivität unter einem Arbeitsbereich/einer Eigenschaft einrichten und beim Konfigurieren des SDK nicht dasselbe einschließen, kann dies dazu führen, dass der `rules.josn` des Standardarbeitsbereichs heruntergeladen wird, wodurch die Mbox unter dem Abschnitt `remoteMboxes` verwendet werden kann.
