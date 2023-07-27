---
title: Identifizierung und Zusammenfassung der Benutzer
description: Identifizierung und Zusammenfassung der Benutzer
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 5%

---

# Identifizierung und Zusammenfassung der Benutzer

## Benutzeridentifizierung

Es gibt mehrere Möglichkeiten, einen Benutzer in [!DNL Adobe Target]. [!UICONTROL Target] verwendet die folgenden Kennungen:

| Feldname | Beschreibung |
| --- | --- |
| `tntID` | Die `tntId` ist die primäre Kennung in [!DNL Target] für einen Benutzer. Sie können diese ID angeben oder [!DNL Target] generiert sie automatisch, wenn die Anforderung keine enthält. |
| `thirdPartyId` | Die `thirdPartyId` ist die Kennung Ihres Unternehmens für den Benutzer, die Sie mit jedem Aufruf senden können. Wenn sich ein Benutzer bei der Site eines Unternehmens anmeldet, erstellt das Unternehmen in der Regel eine ID, die an das Konto, die Treuekarte, die Mitgliedsnummer oder andere für dieses Unternehmen gültige Kennungen des Besuchers gebunden ist. |
| `marketingCloudVisitorId` | Die `marketingCloudVisitorId` dient zum Zusammenführen und Freigeben von Daten zwischen verschiedenen Adobe-Lösungen. Die marketingCloudVisitorId ist für Integrationen mit Adobe Analytics und Adobe Audience Manager erforderlich. |
| `customerIds` | Zusammen mit der Experience Cloud-Besucher-ID wird zusätzlich [Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) und ein authentifizierter Status für jeden Besucher verwendet werden kann. |

## [!DNL Target] ID (tntID)

Die [!DNL Target] ID oder `tntId`, kann als Geräte-ID betrachtet werden. Diese `tntId` automatisch von [!DNL Adobe Target] , wenn sie nicht in der Anfrage angegeben ist. Nachfolgende Anforderungen müssen dies enthalten `tntId` damit der richtige Inhalt an ein Gerät gesendet wird, das von demselben Benutzer verwendet wird.

Der folgende Beispielaufruf zeigt eine Situation, in der ein `tntId` wird nicht übergeben an [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB Java-SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Wenn keine `tntId`, [!DNL Adobe Target] generiert eine `tntId` und stellt ihn in der Antwort wie folgt bereit.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

In diesem Beispiel wurde die `tntId` is `10abf6304b2714215b1fd39a870f01afc.35_0`. Bitte beachten Sie Folgendes `tntId` muss sitzungsübergreifend für denselben Benutzer verwendet werden.

## Drittanbieter-ID (thirdPartyId)

Wenn Ihr Unternehmen zur Identifizierung Ihres Besuchers eine ID verwendet, können Sie `thirdPartyID` um Inhalte bereitzustellen. A `thirdPartyID` ist eine beständige ID, die Ihr Unternehmen zur Identifizierung eines Endbenutzers verwendet, unabhängig davon, ob dieser über Web-, mobile oder IoT-Kanäle mit Ihrem Unternehmen interagiert. Mit anderen Worten, die `thirdPartyId` verweist auf Benutzerprofildaten, die kanalübergreifend verwendet werden können. Sie müssen jedoch die Variable `thirdPartyID` für jeden [!DNL Adobe Target] Bereitstellungs-API-Aufruf, den Sie ausführen.

Der folgende Beispielaufruf zeigt die Verwendung eines `thirdPartyId`.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB Java-SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In diesem Szenario [!DNL Adobe Target] generiert eine `tntId` da sie nicht an den ursprünglichen -Aufruf übergeben wurde, der der bereitgestellten `thirdPartyId`.

## Marketing Cloud-Besucher-ID (marketingCloudVisitorId)

Die `marketingCloudVisitorId` ist eine universelle und beständige ID, mit der Ihre Besucher lösungsübergreifend in der Adobe Experience Cloud identifiziert werden. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in verschiedenen Experience Cloud-Lösungen identifizieren, einschließlich [!DNL Adobe Target], Adobe Analytics und Adobe Audience Manager. Bitte beachten Sie Folgendes: `marketingCloudVisitorId` ist erforderlich bei der Integration [!DNL Target] mit [!DNL Adobe Analytics] und [!DNL Adobe Audience Manager].

Der folgende Beispielaufruf zeigt, wie ein `marketingCloudVisitorId` , der vom Experience Cloud-ID-Dienst abgerufen wurde, wird an [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB Java-SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

In diesem Szenario [!DNL Target] generiert eine `tntId` da sie nicht an den ursprünglichen -Aufruf übergeben wurde, der der bereitgestellten `marketingCloudVisitorId`.

## Kunden-ID (customerIds)

[Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) kann einer Experience Cloud-Besucher-ID hinzugefügt oder mit ihr verknüpft werden. Wann immer `customerIds`, die `marketingCloudVisitorId` müssen ebenfalls angegeben werden. Außerdem kann jeweils ein Authentifizierungsstatus angegeben werden `customerId` für jeden Besucher. Die folgenden Authentifizierungsstatus können verwendet werden:

| Authentifizierungsstatus | Benutzerstatus |
| --- | --- |
| `unknown` | Unbekannt oder noch nie authentifiziert. Dieser Status kann für Szenarien wie jenen verwendet werden, in denen ein Besucher auf Ihre Site gelangt, indem er auf eine Display-Anzeige klickt. |
| `authenticated` | Der Benutzer ist zurzeit in einer aktiven Sitzung auf Ihrer Website oder in Ihrer Applikation authentifiziert. |
| `logged_out` | Der Benutzer war authentifiziert, hat sich dann aber aktiv abgemeldet. Der Benutzer wollte die Verbindung zum authentifizierten Status trennen. Der Benutzer möchte nicht mehr als authentifiziert behandelt werden. |

Beachten Sie, dass die Variable `customerId` sich in einem authentifizierten Status befindet [!DNL Target] referenzieren Sie die Benutzerprofildaten, die gespeichert und mit der customerId verknüpft sind. Wenn die Variable `customerId` ist unbekannt oder `logged_out` -Status, werden sie ignoriert und alle Benutzerprofildaten, die mit dieser verknüpft sein können `customerId` wird nicht für Zielgruppen-Targeting genutzt.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB Java-SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Das obige Beispiel zeigt, wie ein `customerId` mit einer `authenticatedState`. Beim Senden von `customerId`, die `integrationCode`, `id`, und `authenticatedState` sowie `marketingCloudVisitorId` sind erforderlich. Die `integrationCode` ist der Alias der [Kundenattributdatei](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=de) Sie über CRS bereitgestellt haben.

## Zusammengeführtes Profil

Sie können `tntId`, `thirdPartyID`, und `marketingCloudVisitorId` in derselben Anfrage. In diesem Szenario [!DNL Adobe Target] verwaltet die Zuordnung aller IDs und veröffentlicht sie an einen Besucher. Erfahren Sie, wie Profile [zusammengeführt und in Echtzeit synchronisiert](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) unter Verwendung der verschiedenen Kennungen.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB Java-SDK]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Das obige Beispiel zeigt, wie Sie `tntId`, `thirdPartyID`, und `marketingCloudVisitorId` in derselben Anfrage.

## Bucket

Ihren Benutzern wird je nach Einrichtung Ihrer [!DNL Adobe Target] Aktivitäten. In [!DNL Adobe Target], lautet die Zusammenfassung:

* **Deterministisch**: MurmurHash3 wird verwendet, um sicherzustellen, dass Ihr Benutzer zusammengefasst wird und jedes Mal die richtige Variante angezeigt wird, solange die Benutzer-ID konsistent ist.
* **Sticky**: [!DNL Adobe Target] speichert die Variante, die Ihr Benutzer im Benutzerprofil sieht, um sicherzustellen, dass die Variante dem Benutzer sitzungs- und kanalübergreifend angezeigt wird. Varianten und Treue sind bei der Verwendung serverseitiger Entscheidungsfindung garantiert. Bei Verwendung der gerätebezogenen Entscheidungsfindung ist die Zuckigkeit nicht garantiert.

## End-to-End-Bucket-Workflow

Bevor Sie sich mit dem tatsächlichen Bucket-Algorithmus vertraut machen, sollten Sie hervorheben, dass ähnliche Schritte zum Auswählen von Aktivitäten basierend auf ihrem Traffic-Zuordnungsprozentwert sowie zur Auswahl eines Erlebnisses innerhalb einer Aktivität verwendet werden.

### Schritte zur Aktivitätsauswahl

1. Generieren einer Geräte-ID, normalerweise einer UUID
1. Clientcode abrufen
1. Abrufen der Aktivitäts-ID
1. Abrufen des Salzes, bei dem es sich normalerweise um eine Zeichenfolge wie &quot;activity&quot;handelt
1. Hash mit MurmurHash3 berechnen
1. Abrufen des absoluten Werts des Hashs
1. Hash-absoluten Wert durch 10000 teilen
1. Teilen Sie den Rest durch 10000 auf, was einen Wert zwischen 0 und 1 ergeben sollte.
1. Multiplizieren Sie das Ergebnis mit 100 %
1. Vergleichen Sie den Prozentsatz der Aktivitäts-Traffic-Zuordnung mit dem erhaltenen Prozentsatz. Wenn der Traffic-Zuordnungsprozentwert niedriger ist, wird die Aktivität ausgewählt. Andernfalls wird die Aktivität übersprungen.

### Schritte zur Erlebnisauswahl

1. Generieren einer Geräte-ID, normalerweise einer UUID
1. Clientcode abrufen
1. Abrufen der Aktivitäts-ID
1. Erhalten Sie das Salz, das normalerweise eine Zeichenfolge wie &quot;Erlebnis&quot;ist.
1. Hash mit MurmurHash3 berechnen
1. Abrufen des absoluten Werts des Hashs
1. Hash-absoluten Wert durch 10000 teilen
1. Teilen Sie den Rest durch 10000 auf, was einen Wert zwischen 0 und 1 ergeben sollte.
1. Multiplizieren Sie das Ergebnis mit der Gesamtzahl der Erlebnisse in der Aktivität
1. Runden Sie das Ergebnis. Dadurch sollte der Erlebnisindex generiert werden.

### Beispiel

Gehen Sie wie folgt vor:

* Client C mit Clientcode `acmeclient`
* Aktivität A mit ID `1111` und drei Erlebnisse `E1`, `E2`, `E3`
* Erlebnisse weisen die folgende Verteilung auf: `E1` - 33 %, `E2` - 33 %, `E3` - 34 %

Der Auswahlfluss sieht wie folgt aus:

1. Geräte-ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Clientcode `acmeclient`
1. Aktivitäts-ID `1111`
1. Salz `experience`
1. Wert für Hash `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, Hashwert `-919077116`
1. Absoluter Wert des Hashs `919077116`
1. Verbleib nach Division durch 10000, `7116`
1. Wert nach Rest wird durch 10000 geteilt, `0.7116`
1. Ergebnis nach Multiplikation des Werts mit der Gesamtanzahl der Erlebnisse `3 * 0.7116 = 2.1348`
1. Der Erlebnisindex lautet `2`, was das dritte Erlebnis bedeutet, da wir `0` basierte Indizierung.
