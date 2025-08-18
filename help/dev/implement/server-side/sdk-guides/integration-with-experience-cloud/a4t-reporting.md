---
title: Integration mit Experience Cloud A4T-Reporting
description: Integration mit Experience Cloud, A4T-Reporting, Analytics for Target-Integration
keywords: Bereitstellungs-API, serverseitig, serverseitig, Integration, A4T
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: cbae0f1758fb0dee4837e8c237f8617ecb46eb25
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 6%

---

# [!UICONTROL Analytics for Target] (A4T)-Reporting

[!DNL Adobe Target] unterstützt A4T-Reporting sowohl für die geräteinterne Entscheidungsfindung als auch für Server-seitige [!DNL Target]. Es gibt zwei Konfigurationsoptionen zum Aktivieren von A4T-Berichten:

* [!DNL Adobe Target] leitet die Analytics-Payload automatisch an [!DNL Adobe Analytics] weiter oder
* Der Benutzer fordert die Analytics-Payload von [!DNL Adobe Target] an. ([!DNL Adobe Target] gibt die [!DNL Adobe Analytics] Payload an den Aufrufer zurück.)

>[!NOTE]
>
>Die geräteinterne Entscheidungsfindung unterstützt nur A4T-Berichte, von denen [!DNL Adobe Target] die Analytics-Payload automatisch an [!DNL Adobe Analytics] weiterleitet. Das Abrufen der Analytics-Payload aus [!DNL Adobe Target] wird nicht unterstützt.

## Voraussetzungen

1. Konfigurieren Sie die Aktivität in der [!DNL Adobe Target]-Benutzeroberfläche mit [!DNL Adobe Analytics] als Berichtsquelle und stellen Sie sicher, dass die Konten für A4T aktiviert sind.
1. Der API-Benutzer generiert die Adobe-[!UICONTROL Marketing Cloud Visitor ID] und stellt sicher, dass diese ID verfügbar ist, wenn die [!DNL Target] ausgeführt wird.

## [!DNL Adobe Target] leitet die [!DNL Analytics] Payload automatisch weiter

[!DNL Adobe Target] können die Analytics-Payload automatisch an [!DNL Adobe Analytics] weiterleiten, wenn die folgenden Kennungen bereitgestellt werden:

1. `supplementalDataId`: Die ID, die verwendet wird, um zwischen [!DNL Adobe Analytics] und [!DNL Adobe Target] zuzuordnen. Damit [!DNL Adobe Target] und [!DNL Adobe Analytics] Daten korrekt zusammenfügen können, muss dieselbe `supplementalDataId` sowohl an [!DNL Adobe Target] als auch an [!DNL Adobe Analytics] übergeben werden.
1. `trackingServer`: Der [!DNL Adobe Analytics].

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
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
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

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## Benutzer ruft Analytics-Payload von [!DNL Adobe Target] ab

Ein Benutzer kann die [!DNL Adobe Analytics] Payload für eine bestimmte Mbox abrufen und dann über die „Data Insertion [!DNL Adobe Analytics]&quot; an [ ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Wenn eine [!DNL Adobe Target]-Anfrage ausgelöst wird, übergeben Sie `client_side` an das Feld `logging` in der Anfrage. Diese Anfrage gibt eine Payload zurück, wenn die angegebene Mbox in einer Aktivität vorhanden ist, die [!DNL Analytics] als Berichtsquelle verwendet.

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
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
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

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Nachdem Sie `logging = client_side` angegeben haben, erhalten Sie die Payload im mbox-Feld.

Wenn die Antwort von [!DNL Target] etwas in der `analytics -> payload`-Eigenschaft enthält, leiten Sie sie so weiter, wie sie ist, an [!DNL Adobe Analytics]. [!DNL Adobe Analytics] weiß, wie diese Payload verarbeitet wird. Dies kann in einer GET-Anfrage im folgenden Format erfolgen:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/{content_type_num}/{code_ver}/{session}?pe=tnt&tnta={payload}&c.&a.&target.&sessionId={sessionId}&.target&.a&.c&mid={mid}
```

### Parameter und Variablen von Abfragezeichenfolgen

| Feldname | Erforderlich | Beschreibung |
| --- | --- | --- |
| `rsid` | Ja | Die Report Suite-ID |
| `content_type_num` | Ja | Immer auf „0“ festgelegt |
| `code_ver` | Ja | Immer auf „MOBILE-1.0“ eingestellt |
| `session` | Ja | Immer auf „0“ festgelegt |
| `pe` | Ja | Seitenereignis. Immer auf `tnt` gesetzt |
| `tnta` | Ja | [!DNL Analytics] Payload, die von [!DNL Target] Server in `analytics -> payload -> tnta` zurückgegeben wird |
| `sessionId` | Ja | [!DNL Target] Sitzungs-ID der aktuellen Sitzung |
| `mid` | Ja | Marketing Cloud-Besucher-ID |

### Erforderliche Kopfzeilenwerte

| Header-Name | Header-Wert |
| --- | --- |
| Host | Analytics-Datenerfassungs-Server (z. B.: `adobeags421.sc.omtrdc.net`) |

### Beispiel für HTTP-GET-Aufruf zum Einfügen von A4T-Daten

Nicht URL-kodierte Version für bessere Lesbarkeit (Format für API-Aufrufe nicht zu verwenden):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236:0:0|0,253236:0:0|2,253236:0:0|1,253613:0:0|0,253613:0:0|2,253613:0:0|1&c.&a.&target.&sessionId=45c08980-f4b9-4e11-96db-067d58e49f74&.target&.a&.c&pe=tnt&mid=69170113867710665996968872592584719577
```

URL-codierte Version (für API-Aufrufe zu verwendendes Format):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236%3A0%3A0%7C0%2C253236%3A0%3A0%7C2%2C253236%3A0%3A0%7C1%2C253613%3A0%3A0%7C0%2C253613%3A0%3A0%7C2%2C253613%3A0%3A0%7C1&c.%26a.%26target.%26sessionId=45c08980-f4b9-4e11-96db-067d58e49f74%26.target%26.a%26.c&pe=tnt&mid=69170113867710665996968872592584719577 
```
