---
title: Verwenden von getAttributes in [!DNL Adobe Target] mit .NET SDK
description: Erfahren Sie, wie Sie mit getAttributes() Experimente und personalisierte Erlebnisse aus abrufen  [!DNL Target]  Attributwerte extrahieren können.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 9%

---

# Abrufen von Attributen (.NET)

## Beschreibung

`GetAttributes()` wird verwendet, um Experimente und personalisierte Erlebnisse aus [!DNL Target] abzurufen und Attributwerte zu extrahieren.

## Methode

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Parameter

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| targetRequest | targetDeliveryRequest | Nein | null  | Dieselbe [!DNL Target], die für „Angebote [&quot; verwendet &#x200B;](get-offers.md) |
| mboxNames | Parameterzeichenfolge[] | Nein | null  | Ein Parameter-Array mit Mbox-Namen |

## Ergebnis

Ein `TargetAttributes` wird von `TargetClient.GetAttributes()` zurückgegeben, das die folgenden Eigenschaften und Methoden aufweist:

| Eigenschaft/Methode | Rückgabetyp | Beschreibung |
| --- | --- | --- |
| Antwort | targetDeliveryResponse | Gibt das Antwortobjekt zurück, das normalerweise von „Angebote [&quot; zurückgegeben &#x200B;](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Gibt ein Wörterbuch der Wörterbücher mit Schlüsselwertpaaren zurück, die nach Mbox-Namen gruppiert sind |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Gibt ein Wörterbuch mit Schlüsselwertpaaren für die bereitgestellte Mbox zurück. |
| GetBoolean(mboxName, key, defaultValue) | boolesch | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| GetString(mboxName, key, defaultValue) | string | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| GetInteger(mboxName, key, defaultValue) | int | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| GetDouble(mboxName, key, defaultValue) | Doppelte Genauigkeit | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |
| GetValue(mboxName, key, defaultValue) | T   | Gibt den Wert für einen angegebenen Mbox-Namen und einen Attributschlüssel zurück. |

## Beispiel

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
