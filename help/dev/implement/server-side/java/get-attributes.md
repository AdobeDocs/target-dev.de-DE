---
title: Verwenden Sie getAttributes in [!DNL Adobe Target] mit dem Java-SDK
description: Erfahren Sie, wie Sie mit getAttributes() Experimente und personalisierte Erlebnisse abrufen können. [!DNL Target] und extrahieren Sie Attributwerte.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# Abrufen von Attributen (Java)

## Beschreibung

`getAttributes()` wird zum Abrufen von Experimenten und personalisierten Erlebnissen aus [!DNL Target] und extrahieren Sie Attributwerte.

## Methode

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Parameter

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Ja | Keine | Dieselbe Zielanforderung für [Angebote &#x200B;](get-offers.md) |
| mboxNames | var-args-Array | Nein | Keine | Ein var-args-Array mit Mbox-Namen |


## Ergebnis

Ein `Attributes` -Objekt zurückgegeben von `TargetClient.getAttributes()` die die folgenden Methoden aufweist:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| getBoolean(mboxName, key) | Boolesch | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| getString(mboxName, key) | Zeichenfolge | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| getInteger(mboxName, key) | Ganzzahl | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| getDouble(mboxName, key) | Doppelt | Gibt den Wert für einen angegebenen Mbox-Namen und Attributschlüssel aus |
| toMboxMap(mboxName) | Landkarte | Gibt eine einfache Zuordnung mit Schlüsselwertpaaren zurück |
| getResponse() | TargetDeliveryResponse | Gibt das Antwortobjekt zurück, das normalerweise von getOffers zurückgegeben wird |

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
