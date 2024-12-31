---
title: Verwenden von getAttributes in  [!DNL Adobe Target]  mit der Java-SDK
description: Erfahren Sie, wie Sie mit getAttributes() Experimente und personalisierte Erlebnisse aus abrufen  [!DNL Target]  Attributwerte extrahieren können.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# Abrufen von Attributen (Java)

## Beschreibung

`getAttributes()` wird verwendet, um Experimente und personalisierte Erlebnisse aus [!DNL Target] abzurufen und Attributwerte zu extrahieren.

## Methode

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parameter

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| targetRequest | targetDeliveryRequest | Ja | Keine | &#x200B; Dieselbe Zielgruppenanfrage wie für „Angebote [&quot; ](get-offers.md) |
| mboxNames | var-args-Array | Nein | Keine | Ein var-args-Array von mbox-Namen |


## Ergebnis

Ein `Attributes` wird von `TargetClient.getAttributes()` zurückgegeben, das die folgenden Methoden aufweist:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| getBoolean(mboxName, key) | Boolesch | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| getString(mboxName, key) | Zeichenfolge | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| getInteger(mboxName, key) | Ganzzahl | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| getDouble(mboxName, key) | Doppelt | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| toMboxMap(mboxName) | Landkarte | Gibt eine einfache Zuordnung mit Schlüsselwertpaaren zurück. |
| getResponse() | targetDeliveryResponse | Gibt das Antwortobjekt zurück, das normalerweise von getOffers zurückgegeben wird |

## Beispiel

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
