---
title: Verwenden Sie getOffers() in [!DNL Adobe Target] bei Verwendung des Java-SDK.
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis aus  [!DNL Adobe Target] abrufen können.
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 13%

---

# Angebote abrufen (Java)

## Beschreibung

`getOffers()` wird verwendet, um eine Entscheidung auszuführen und ein Erlebnis aus [!DNL Adobe Target] abzurufen.

## Methode

### getOffers

Die Signatur der Methode `TargetClient.getOffers` wird wie folgt angezeigt.

**Anfrage**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest wird mit `TargetDeliveryRequest.builder` erstellt.

**Antwort**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Parameter

Das Objekt `[!UICONTROL TargetDeliveryRequestBuilder]` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| Kontext | Kontext | Ja | Gibt den Kontext für die Anforderung an |
| sessionId |  | Zeichenfolge | Nein | Wird zum Verknüpfen mehrerer [!DNL Target] -Anforderungen verwendet |
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
| mcId | Zeichenfolge | Nein | Dient zum Zusammenführen und Freigeben von Daten zwischen verschiedenen [!DNL Adobe]-Lösungen (ECID). Aus targetCookies abgerufen. Automatisch generiert, wenn nicht angegeben. |
| trackingServer | Zeichenfolge | Nein | Der Adobe Analytics-Server, damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen. |
| trackingServerSecure | Zeichenfolge | Nein | Die [!UICONTROL Adobe Analytics Secure Server], damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen. |
| decisioningMethod | DecisioningMethod | Nein | Kann verwendet werden, um explizit ON_DEVICE- oder HYBRID-Entscheidungsmethode für geräteinterne Entscheidungen festzulegen |

Die Werte der einzelnen Felder sollten der Anforderungsspezifikation *[!UICONTROL Target View Delivery API]* entsprechen. Weitere Informationen zum *[!UICONTROL Target View Delivery API]* finden Sie unter [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Antwort

Die von `TargetClient.getOffers(` zurückgegebene `TargetDeliveryResponse` hat die folgende Struktur:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | TargetDeliveryRequest-&#x200B; | *[!DNL Target]* Anfrage |
| response | DeliveryResponse | *[!DNL Target]* Antwort |
| Cookies | Liste | Liste der Sitzungsmetadaten für diesen Benutzer. Muss in der nächsten Target-Anfrage für diesen Benutzer übergeben werden. |
| visitorState | Landkarte | Besucherstatus, der clientseitig für die Verwendung durch die Besucher-API festgelegt wird |
| responseStatus | ResponseStatus | Ein Objekt, das den Status der Antwort darstellt |

Der Wert `ResponseStatus` in der Antwort enthält die folgenden Felder:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| status | int | HTTP-Status zurückgegeben von [!DNL Target] |
| message | Zeichenfolge | Statusmeldung bei HTTP-Status nicht 200 |
| remoteMboxes | Liste von Zeichenfolgen | Wird für Entscheidungen auf dem Gerät verwendet. Enthält eine Liste von Mboxes mit Remote-Aktivitäten, die nicht vollständig auf dem Gerät entschieden werden können. |
| remoteViews | Liste von Zeichenfolgen | Wird für Entscheidungen auf dem Gerät verwendet. Enthält eine Liste von Ansichten mit Remote-Aktivitäten, die nicht vollständig auf dem Gerät entschieden werden können. |

Das `TargetCookie` -Objekt, das zum Speichern von Daten für die Benutzersitzung verwendet wird, weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | Zeichenfolge | Cookie-Name |
| value | Zeichenfolge | Cookie-Wert, wird der Wert in eine Zeichenfolge konvertiert |
| maxAge | Nummer | Die Option &quot;maxAge&quot;ist eine praktische Option, um die Ablaufzeit relativ zur aktuellen Zeit in Sekunden festzulegen. |

Du brauchst dir keine Sorgen zu machen, dass die Cookies ablaufen. Target verarbeitet maxAge im SDK.

## Beispiel

**Anfrage**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**Antwort**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
