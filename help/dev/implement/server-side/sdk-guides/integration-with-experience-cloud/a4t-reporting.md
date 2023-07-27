---
title: Integration in Experience Cloud A4T Reporting
description: Integration in Experience Cloud, A4T-Reporting, Analytics for Target-Integration
keywords: Bereitstellungs-API, Server-seitig, serverseitig, Integration, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 8%

---

# Berichterstellung von Analytics for Target (A4T)

[!DNL Adobe Target] unterstützt A4T-Berichte für Entscheidungen auf dem Gerät und für serverseitige Target-Aktivitäten. Es gibt zwei Konfigurationsoptionen für die Aktivierung der A4T-Berichterstellung:

* [!DNL Adobe Target] leitet die Analytics-Nutzlast automatisch an [!DNL Adobe Analytics]oder
* Der Benutzer fordert die Analytics-Nutzlast von [!DNL Adobe Target]. ([!DNL Adobe Target] gibt die [!DNL Adobe Analytics] Nutzlast an den Aufrufer zurück.)

>[!NOTE]
>
>Die Entscheidungsfindung auf dem Gerät unterstützt nur A4T-Berichte, von denen [!DNL Adobe Target] leitet die Analytics-Nutzlast automatisch an [!DNL Adobe Analytics]. Analytics-Nutzlast abrufen von [!DNL Adobe Target] wird nicht unterstützt.

## Voraussetzungen

1. Konfigurieren Sie die Aktivität im [!DNL Adobe Target] Benutzeroberfläche mit [!DNL Adobe Analytics] als Berichtsquelle verwenden und sicherstellen, dass die Konten für A4T aktiviert sind.
1. Der API-Benutzer generiert die Adobe Marketing Cloud-Besucher-ID und stellt sicher, dass diese ID verfügbar ist, wenn die Target-Anforderung ausgeführt wird.

## [!DNL Adobe Target] leitet die Analytics-Payload automatisch weiter

[!DNL Adobe Target] kann die Analyse-Payload automatisch an weiterleiten [!DNL Adobe Analytics] wenn die folgenden Kennungen angegeben sind:

1. `supplementalDataId`: Die ID, die zum Zuordnen zwischen verwendet wird [!DNL Adobe Analytics] und [!DNL Adobe Target]. Zur [!DNL Adobe Target] und [!DNL Adobe Analytics] zum korrekten Zusammenfügen von Daten, das gleiche `supplementalDataId` muss an beide übergeben werden [!DNL Adobe Target] und [!DNL Adobe Analytics].
1. `trackingServer`: Die [!DNL Adobe Analytics] Server.

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

>[!TAB Java ]

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

## Benutzer ruft die Analytics-Nutzlast von ab [!DNL Adobe Target]

Ein Benutzer kann die [!DNL Adobe Analytics] Nutzlast für eine bestimmte Mbox und anschließender Versand an [!DNL Adobe Analytics] über die [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Wenn ein [!DNL Adobe Target] Anfrage wird ausgelöst, Übergeben `client_side` der `logging` in der Anfrage. Dadurch wird eine Payload zurückgegeben, wenn die angegebene Mbox in einer Aktivität vorhanden ist, die Analytics als Berichtsquelle verwendet.

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

>[!TAB Java ]

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

Einmal angegeben `logging = client_side`, erhalten Sie die Payload im mbox -Feld.

Wenn die Antwort von Target etwas im `analytics -> payload` -Eigenschaft, leiten Sie sie wie gewünscht an [!DNL Adobe Analytics]. [!DNL Adobe Analytics] weiß, wie diese Payload verarbeitet wird. Dies kann in einer GET-Anfrage im folgenden Format erfolgen:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Abfragezeichenfolgenparameter und Variablen

| Feldname | Erforderlich | Beschreibung |
| --- | --- | --- |
| `rsid` | Ja | Die Report Suite-ID |
| `pe` | Ja | Seitenereignis. Immer auf `tnt` |
| `tnta` | Ja | Analytics-Nutzlast, die vom Target-Server in zurückgegeben wird `analytics -> payload -> tnta` |
| `mid` | Ja | Marketing Cloud-Besucher-ID |

### Erforderliche Kopfzeilenwerte

| Header-Name | Header-Wert |
| --- | --- |
| Host | Analytics-Datenerfassungsserver (z. B.: `adobeags421.sc.omtrdc.net`) |

### Beispiel für einen HTTP-Abruf zum Einfügen von A4T-Daten

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
