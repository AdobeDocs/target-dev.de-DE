---
title: Benutzeridentifizierung und Bucketing
description: Benutzeridentifizierung und Bucketing
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# Benutzeridentifizierung und Bucketing

## Benutzeridentifizierung

Es gibt mehrere Möglichkeiten, einen Benutzer innerhalb von [!DNL Adobe Target] zu identifizieren. [!UICONTROL Target] verwendet die folgenden Kennungen:

| Feldname | Beschreibung |
| --- | --- |
| `tntID` | Der `tntId` ist die primäre Kennung in [!DNL Target] für einen Benutzer. Sie können diese ID bereitstellen oder [!DNL Target] generiert sie automatisch, wenn die Anfrage keine enthält. |
| `thirdPartyId` | Der `thirdPartyId` ist die Kennung des Benutzers in Ihrem Unternehmen, die Sie mit jedem Aufruf senden können. Wenn sich ein(e) Benutzende(r) auf der Website eines Unternehmens anmeldet, erstellt das Unternehmen normalerweise eine ID, die mit dem Konto, der Treuekarte, der Mitgliedschaftsnummer oder anderen Kennungen des/der Besuchenden für dieses Unternehmen verknüpft ist. |
| `marketingCloudVisitorId` | Die `marketingCloudVisitorId` wird verwendet, um Daten zwischen verschiedenen Adobe-Lösungen zusammenzuführen und freizugeben. Die marketingCloudVisitorId ist für Integrationen mit Adobe Analytics und Adobe Audience Manager erforderlich. |
| `customerIds` | Neben der Experience Cloud-Besucher-ID können auch zusätzliche [Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) und ein Authentifizierungsstatus für jeden Besucher verwendet werden. |

## [!DNL Target]-ID (tntID)

Die [!DNL Target]-ID oder `tntId` kann als Geräte-ID betrachtet werden. Diese `tntId` wird automatisch von [!DNL Adobe Target] generiert, wenn sie nicht in der Anfrage angegeben ist. Nachfolgende Anfragen müssen diese `tntId` enthalten, damit der richtige Inhalt an ein Gerät gesendet werden kann, das vom selben Benutzer verwendet wird.

Der folgende Beispielaufruf zeigt eine Situation, in der ein `tntId` nicht an [!DNL Target] übergeben wird.

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

>[!TAB Java SDK]

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

Wenn keine `tntId` vorhanden ist, generiert [!DNL Adobe Target] eine `tntId` und stellt sie in der Antwort wie folgt bereit.

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

In diesem Beispiel wird der generierte `tntId` `10abf6304b2714215b1fd39a870f01afc.35_0`. Beachten Sie, dass diese `tntId` sitzungsübergreifend für denselben Benutzer verwendet werden muss.

## Drittanbieter-ID (thirdPartyId)

Wenn Ihr Unternehmen eine ID verwendet, um Ihren Besucher zu identifizieren, können Sie `thirdPartyID` verwenden, um Inhalte bereitzustellen. Eine `thirdPartyID` ist eine persistente ID, mit der Ihr Unternehmen Endbenutzende identifiziert, unabhängig davon, ob diese über Web-, Mobil- oder IoT-Kanäle mit Ihrem Unternehmen interagieren. Mit anderen Worten, die `thirdPartyId` verweist auf Benutzerprofildaten, die kanalübergreifend verwendet werden können. Sie müssen jedoch die `thirdPartyID` für jeden Aufruf der [!DNL Adobe Target]-Bereitstellungs-API angeben.

Der folgende Beispielaufruf veranschaulicht die Verwendung eines `thirdPartyId`.

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

>[!TAB Java SDK]

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

In diesem Szenario generiert [!DNL Adobe Target] eine `tntId`, da sie nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `thirdPartyId` zugeordnet wird.

## Marketing Cloud-Besucher-ID (marketingCloudVisitorId)

Die `marketingCloudVisitorId` ist eine universelle und persistente ID, die Ihre Besucher über alle Adobe Experience Cloud-Lösungen hinweg identifiziert. Wenn Ihr Unternehmen den ID-Service implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in verschiedenen Experience Cloud-Lösungen identifizieren, einschließlich [!DNL Adobe Target], Adobe Analytics und Adobe Audience Manager. Beachten Sie, dass die `marketingCloudVisitorId` bei der Integration von [!DNL Target] mit [!DNL Adobe Analytics] und [!DNL Adobe Audience Manager] erforderlich ist.

Der folgende Beispielaufruf zeigt, wie ein `marketingCloudVisitorId`, das vom Experience Cloud-ID-Service abgerufen wurde, an [!DNL Target] übergeben wird.

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

>[!TAB Java SDK]

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

In diesem Szenario generiert [!DNL Target] eine `tntId`, da sie nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `marketingCloudVisitorId` zugeordnet wird.

## Kunden-ID (customerIds)

[Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=de) können einer Experience Cloud-Besucher-ID hinzugefügt oder mit ihr verknüpft werden. Bei jedem Versand von `customerIds` muss auch die `marketingCloudVisitorId` angegeben werden. Darüber hinaus kann für jeden Besucher ein Authentifizierungsstatus zusammen mit jedem `customerId` angegeben werden. Die folgenden Authentifizierungsstatus können verwendet werden:

| Authentifizierungsstatus | Benutzerstatus |
| --- | --- |
| `unknown` | Unbekannt oder nie authentifiziert. Dieser Status kann für Szenarien wie das Szenario verwendet werden, in dem ein Besucher durch Klicken auf eine Display-Anzeige auf Ihre Site gelangt. |
| `authenticated` | Der Benutzer ist zurzeit in einer aktiven Sitzung auf Ihrer Website oder in Ihrer Applikation authentifiziert. |
| `logged_out` | Der Benutzer war authentifiziert, hat sich dann aber aktiv abgemeldet. Der Benutzer beabsichtigt, die Verbindung zum authentifizierten Status zu trennen. Der Benutzer möchte nicht mehr als authentifiziert behandelt werden. |

Beachten Sie, dass nur dann auf die Benutzerprofildaten verwiesen wird, wenn sich die `customerId` [!DNL Target] im authentifizierten Zustand befindet, die gespeichert und mit der customerId verknüpft sind. Wenn sich die `customerId` in einem unbekannten oder `logged_out` Status befindet, wird sie ignoriert, und alle Benutzerprofildaten, die mit dieser `customerId` verknüpft sind, werden nicht für das Audience-Targeting genutzt.

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

>[!TAB Java SDK]

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

Das obige Beispiel zeigt, wie ein `customerId` mit einem `authenticatedState` gesendet wird. Beim Senden eines `customerId` sind die `integrationCode`, `id` und `authenticatedState` sowie die `marketingCloudVisitorId` erforderlich. Der `integrationCode` ist der Alias der [Kundenattributdatei), ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=de) Sie über CRS bereitgestellt haben.

## Zusammengeführtes Profil

Sie können `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anfrage kombinieren. In diesem Szenario verwaltet [!DNL Adobe Target] die Zuordnung aller dieser IDs und heftet sie an einen Besucher an. Erfahren Sie, wie Profile mithilfe [ verschiedenen Kennungen in Echtzeit zusammengeführt ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=de) synchronisiert werden.

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

>[!TAB Java SDK]

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

Das obige Beispiel zeigt, wie Sie `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anfrage kombinieren können.

## Bucketing

Je nachdem, wie Sie Ihre [!DNL Adobe Target]-Aktivitäten einrichten, werden Ihre Benutzerinnen und Benutzer in Gruppen zusammengefasst, um ein Erlebnis zu sehen. In [!DNL Adobe Target] ist Bucketing:

* **Deterministisch**: MurmurHash3 wird verwendet, um sicherzustellen, dass Ihre Benutzenden in Buckets zusammengefasst sind und jedes Mal die richtige Variante sehen, solange die Benutzer-ID konsistent ist.
* **Sticky**: [!DNL Adobe Target] speichert die Variante, die Ihr Benutzer im Benutzerprofil sieht, um sicherzustellen, dass die Variante diesem Benutzer über Sitzungen und Kanäle hinweg konsistent angezeigt wird. Bei der Verwendung der Server-seitigen Entscheidungsfindung sind Variationen und Konsistenz garantiert. Bei Verwendung der geräteinternen Entscheidungsfindung ist die Konsistenz nicht garantiert.

## End-to-End-Bucketing-Workflow

Bevor wir in den tatsächlichen Bucketing-Algorithmus eintauchen, müssen Sie betonen, dass ähnliche Schritte sowohl zur Auswahl von Aktivitäten basierend auf ihrem Traffic-Zuordnungsprozentsatz als auch zur Auswahl eines Erlebnisses innerhalb einer Aktivität verwendet werden.

### Schritte zur Aktivitätsauswahl

1. Generieren einer Geräte-ID, normalerweise einer UUID
1. Client-Code abrufen
1. Abrufen der Aktivitäts-ID
1. Holen Sie sich das Salz, das normalerweise eine Zeichenfolge wie „Aktivität“ ist
1. Berechnen des Hash mithilfe von MurmurHash3
1. Absoluten Wert des Hash abrufen
1. Dividieren des absoluten Hash-Werts durch 10000
1. Teilen Sie den Rest durch 10000, wodurch ein Wert zwischen 0 und 1 entsteht.
1. Multiplizieren Sie das Ergebnis mit 100 %
1. Vergleich des Prozentsatzes der Traffic-Zuordnung der Aktivität mit dem abgerufenen Prozentsatz. Wenn der Prozentsatz der Traffic-Zuordnung niedriger ist, wird die Aktivität ausgewählt. Andernfalls wird die Aktivität übersprungen.

### Schritte zur Erlebnisauswahl

1. Generieren einer Geräte-ID, normalerweise einer UUID
1. Client-Code abrufen
1. Abrufen der Aktivitäts-ID
1. Holen Sie sich das Salz, was normalerweise eine Zeichenfolge wie „Erlebnis“ ist
1. Berechnen des Hash mithilfe von MurmurHash3
1. Absoluten Wert des Hash abrufen
1. Dividieren des absoluten Hash-Werts durch 10000
1. Teilen Sie den Rest durch 10000, wodurch ein Wert zwischen 0 und 1 entsteht.
1. Multiplizieren Sie das Ergebnis mit der Gesamtzahl der Erlebnisse innerhalb der Aktivität.
1. Runden Sie das Ergebnis ab. Dadurch sollte der Erlebnisindex erstellt werden.

### Beispiel

Angenommen, Folgendes:

* Client C mit Client-Code `acmeclient`
* Aktivität A mit ID `1111` und drei Erlebnissen `E1`, `E2`, `E3`
* Erfahrungen haben folgende Verteilung: `E1` - 33 %, `E2` - 33 %, `E3` - 34 %

Der Auswahlfluss sieht wie folgt aus:

1. Geräte-ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. Client-Code-`acmeclient`
1. Aktivitäts-ID `1111`
1. `experience`
1. Wert in Hash-`acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, Hash-Wert-`-919077116`
1. Absoluter Wert des Hash-`919077116`
1. Rest nach Division durch 10000, `7116`
1. Wert nach Rest wird durch 10000 dividiert, `0.7116`
1. Ergebnis nach Multiplikation des Werts mit der Gesamtzahl der `3 * 0.7116 = 2.1348` Erlebnisse
1. Der Erlebnis-Index ist `2`, was das dritte Erlebnis bedeutet, da wir die `0` Indizierung verwenden.
