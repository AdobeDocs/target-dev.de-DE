---
title: Verwenden von getOffers() in  [!DNL Adobe Target]  bei Verwendung von .NET SDK
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis aus abrufen können [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
TQID: https://experienceleague.adobe.com/T-oUyDgCJZ8hqQZgCb3-Z-d9WeMaffwq8krMHhGvYlI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 576
ht-degree: 14%

---

# Angebote abrufen (.NET)

## Beschreibung

`GetOffers()` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.

## Methode

`TargetClient.GetOffers` Methodensignatur.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` wird mithilfe von `TargetDeliveryRequest.Builder` erstellt.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Parameter

Das `TargetDeliveryRequest.Builder`-Objekt hat die folgende Struktur:

| Name | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| Kontext | Kontext | Ja | Gibt den Kontext für die Anfrage an |
| sessionId | Zeichenfolge | Nein | Wird zum Verknüpfen mehrerer [!DNL Target] verwendet |
| thirdPartyId | Zeichenfolge | Nein | Die Kennung Ihres Unternehmens für den Benutzer, die Sie mit jedem Aufruf senden können |
| Cookies | Liste | Nein | Liste der Cookies, die in der vorherigen [!DNL Target]-Anfrage desselben Benutzers zurückgegeben wurden. |
| customerIds | Landkarte | Nein | Kunden-IDs im VisitorId-kompatiblen Format |
| vollziehen | Anfrage ausführen | Nein | Auszuführende PageLoad- oder Mboxes-Anfrage. Wird sofort Server-seitig ausgewertet |
| Vorabruf | PrefetchRequest | Nein | Ansichten, PageLoad- oder Mboxes-Anfragen zum vorherigen Abrufen. Gibt mit Benachrichtigungs-Token zurück, das bei der Konversion zurückgegeben wird. |
| Benachrichtigungen | Liste | Nein | Ermöglicht das Senden von Benachrichtigungen darüber, welche vorab abgerufenen Inhalte angezeigt wurden |
| requestId | Zeichenfolge | Nein | Die Anfrage-ID, die in der Antwort zurückgegeben wird. Wird automatisch generiert, wenn nicht vorhanden. |
| impressionId | Zeichenfolge | Nein | Wenn vorhanden, erhöhen zweite und nachfolgende Anfragen mit derselben ID nicht die Impressions zu Aktivitäten/Metriken. Wird automatisch generiert, wenn nicht vorhanden. |
| environmentId | Lang | Nein | Gültige Client-Umgebungs-ID. Wenn kein Host angegeben ist, wird er anhand des bereitgestellten Hosts bestimmt. |
| Eigenschaft | Eigenschaft | Nein | Gibt die at_property über das Token-Feld an. Er kann zur Steuerung des Versandumfangs verwendet werden. |
| Spur | Spur | Nein | Aktiviert die Ablaufverfolgung für die Bereitstellungs-API. |
| qaMode | QAMode | Nein | Verwenden Sie dieses Objekt, um den QA-Modus in der Anfrage zu aktivieren. |
| locationHint | Zeichenfolge | Nein | [!DNL Target] Edge-Cluster-Standorthinweis. Wird verwendet, um den jeweiligen Edge-Cluster für diese Anfrage anzusprechen. |
| Besucher | Besucher | Nein | Wird verwendet, um ein benutzerdefiniertes Besucher-API-Objekt bereitzustellen. |
| id | VisitorId | Nein | Objekt, das die Kennungen für den Besucher enthält. Beispiel: tntId, thirdPartyId, mcId, customerIds. |
| Experience Cloud | Experience Cloud | Nein | Gibt Integrationen mit Audience Manager und Analytics an. Wird automatisch mithilfe von Cookies ausgefüllt, sofern keine Cookies angegeben wurden. |
| tntId | Zeichenfolge | Nein | Primäre Kennung in [!DNL Target] für einen Benutzer. Aus targetCookies abgerufen. Wird automatisch generiert, wenn nicht angegeben. |
| mcId | Zeichenfolge | Nein | Wird zum Zusammenführen und Freigeben von Daten zwischen verschiedenen Adobe-Lösungen (ECID) verwendet. Aus targetCookies abgerufen. Wird automatisch generiert, wenn nicht angegeben. |
| trackingServer | Zeichenfolge | Nein | Der Adobe Analytics-Server, damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen können. |
| trackingServerSecure | Zeichenfolge | Nein | Der [!UICONTROL Adobe Analytics Secure Server], damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen können. |
| decisioningMethod | decisioningMethod | Nein | Kann verwendet werden, um die Entscheidungsmethode ON_DEVICE oder HYBRID explizit für On-Device Decisioning festzulegen |

Die Werte der einzelnen Felder sollten der Anforderungsspezifikation [Target-Bereitstellungs](/help/dev/implement/delivery-api/overview.md) entsprechen.

## Antwort

Die von `TargetClient.GetOffers()` zurückgegebene `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | targetDeliveryRequest&#x200B; | [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) Anfrage |
| Antwort | deliveryResponse&#x200B; | [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md)* Antwort |
| Status | HttpStatusCode | HTTP-Status-Code der Antwort |
| Nachricht | string | Antwort-Statusmeldung oder Fehlermeldung |
| Positionen | Positionen | [!DNL Target] Ortsnamen, einschließlich des globalen Mbox-Namens und der Mboxes/Ansichten, für die nur Remote Decisioning verfügbar ist |
| Cookies abrufen | Wörterbuch | Gibt ein Wörterbuch der Sitzungsmetadaten für diesen Benutzer zurück. Dies muss bei der nächsten [!DNL Target] für diesen Benutzer übergeben werden. |
| Bundesland des Besuchers | IDictionary | Besucherstatus, der Client-seitig für die Initialisierung der Besucher-API-JavaScript-Bibliothek festgelegt wird |

Das `TargetCookie` -Objekt, das zum Speichern von Daten für Benutzersitzungen verwendet wird, weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Name | string | Cookie-Name |
| Wert | string | Cookie-Wert |
| MaxAge | int | Die Option &quot;`MaxAge`&quot; ist eine praktische Option zum Festlegen von „Läuft ab“ relativ zur aktuellen Zeit in Sekunden |

Sie müssen sich keine Sorgen machen, dass die Cookies ablaufen. [!DNL Target] verarbeitet `MaxAge` innerhalb der SDK.

## Beispiel

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
