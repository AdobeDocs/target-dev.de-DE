---
title: Verwenden Sie getOffers() in [!DNL Adobe Target] bei der Verwendung des .NET SDK.
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis aus  [!DNL Adobe Target] abrufen können.
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 14%

---

# Angebote abrufen (.NET)

## Beschreibung

`GetOffers()` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.

## Methode

`TargetClient.GetOffers` Methodenunterschrift.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` wird mit `TargetDeliveryRequest.Builder` erstellt.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Parameter

Das Objekt `TargetDeliveryRequest.Builder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| Kontext | Kontext | Ja | Gibt den Kontext für die Anforderung an |
| sessionId | Zeichenfolge | Nein | Wird zum Verknüpfen mehrerer [!DNL Target] -Anforderungen verwendet |
| thirdPartyId | Zeichenfolge | Nein | Die Kennung Ihres Unternehmens für den Benutzer, den Sie bei jedem Aufruf senden können |
| Cookies | Liste | Nein | Liste der Cookies, die in der vorherigen [!DNL Target] -Anfrage desselben Benutzers zurückgegeben wurden. |
| customerIds | Landkarte | Nein | Kunden-IDs im mit VisitorId kompatiblen Format |
| execute | ExecuteRequest | Nein | PageLoad - oder Mbox-Anfrage zur Ausführung. wird sofort serverseitig ausgewertet |
| Vorabruf | PrefetchRequest | Nein | Anfragen für Ansichten, PageLoad oder Mboxes zum Vorabruf. Gibt mit dem Benachrichtigungstoken zurück, das bei der Konvertierung zurückgegeben wird. |
| Benachrichtigungen | Liste | Nein | Wird verwendet, um Benachrichtigungen darüber zu senden, welcher vorabgerufene Inhalt angezeigt wurde |
| requestId | Zeichenfolge | Nein | Die Anfrage-ID, die in der Antwort zurückgegeben wird. Wird automatisch generiert, wenn nicht vorhanden. |
| impressionId | Zeichenfolge | Nein | Falls vorhanden, werden bei zweiten und nachfolgenden Anfragen mit derselben ID die Impressionen nicht zu Aktivitäten/Metriken erhöht. Wird automatisch generiert, wenn nicht vorhanden. |
| environmentId | Lang | Nein | Gültige Client-Umgebungs-ID. Wenn kein spezifizierter Host angegeben ist, wird er auf Grundlage des bereitgestellten Hosts bestimmt. |
| property | Eigenschaft | Nein | Gibt die at_property über das Tokenfeld an. Er kann verwendet werden, um den Umfang des Versands zu steuern. |
| trace | Spur | Nein | Aktiviert Trace für die Bereitstellungs-API. |
| qaMode | QAMode | Nein | Verwenden Sie dieses Objekt, um den QA-Modus in der Anfrage zu aktivieren. |
| locationHint | Zeichenfolge | Nein | [!DNL Target] Edge Cluster-Standorthinweis. Wird für das Targeting des angegebenen Edge-Clusters für diese Anfrage verwendet. |
| Besucher | Besucher | Nein | Wird zur Bereitstellung eines benutzerdefinierten Besucher-API-Objekts verwendet. |
| id | VisitorId | Nein | Objekt, das die IDs für den Besucher enthält. z. tntId, thirdParyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | Nein | Gibt Integrationen mit Audience Manager und Analytics an. Wird automatisch mit Cookies ausgefüllt, falls nicht angegeben. |
| tntId | Zeichenfolge | Nein | Primäre Kennung in [!DNL Target] für einen Benutzer. Aus targetCookies abgerufen. Automatisch generiert, wenn nicht angegeben. |
| mcId | Zeichenfolge | Nein | Dient zum Zusammenführen und Freigeben von Daten zwischen verschiedenen Adobe-Lösungen (ECID). Aus targetCookies abgerufen. Automatisch generiert, wenn nicht angegeben. |
| trackingServer | Zeichenfolge | Nein | Der Adobe Analytics-Server, damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen. |
| trackingServerSecure | Zeichenfolge | Nein | Die [!UICONTROL Adobe Analytics Secure Server], damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen. |
| decisioningMethod | DecisioningMethod | Nein | Kann verwendet werden, um explizit ON_DEVICE- oder HYBRID-Entscheidungsmethode für geräteinterne Entscheidungen festzulegen |

Die Werte der einzelnen Felder sollten der Anforderungsspezifikation für die [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) entsprechen.

## Antwort

Die von `TargetClient.GetOffers()` zurückgegebene `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | TargetDeliveryRequest-&#x200B; | [Anfrage zur Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) |
| Antwort | DeliveryResponse &#x200B; | Antwort [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md)* |
| Status | HttpStatusCode | Antwort-HTTP-Statuscode |
| Nachricht | string | Nachricht zum Antwortstatus oder Fehlermeldung |
| Positionen | Positionen | [!DNL Target] Ortsnamen, einschließlich globaler Mbox-Name und Mboxes/Ansichten, für die nur Remote-Entscheidungen verfügbar sind |
| GetCookies | Wörterbuch | Gibt ein Wörterbuch mit Sitzungsmetadaten für diesen Benutzer zurück. Dies muss in der nächsten [!DNL Target] -Anfrage für diesen Benutzer übergeben werden. |
| VisitorState | IDictionary | Besucherstatus, der clientseitig für die Initialisierung der Javascript-Bibliothek der Besucher-API festgelegt wird |

Das `TargetCookie` -Objekt, das zum Speichern von Daten für die Benutzersitzung verwendet wird, weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Name | string | Cookie-Name |
| Wert | string | Cookie-Wert |
| MaxAge | int | Mit der Option `MaxAge` können Sie die Option Läuft ab relativ zur aktuellen Zeit in Sekunden festlegen. |

Du brauchst dir keine Sorgen zu machen, dass die Cookies ablaufen. [!DNL Target] verarbeitet `MaxAge` im SDK.

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
