---
title: Verwenden von getOffers() in  [!DNL Adobe Target]  bei Verwendung der Java-SDK
description: Erfahren Sie, wie Sie mit getOffers() eine Entscheidung ausführen und ein Erlebnis aus abrufen können [!DNL Adobe Target].
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

Die Signatur der `TargetClient.getOffers`-Methode wird wie folgt angezeigt.

**Anfrage**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest wird mithilfe von `TargetDeliveryRequest.builder` erstellt.

**Antwort**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Parameter

Das `[!UICONTROL TargetDeliveryRequestBuilder]`-Objekt hat die folgende Struktur:

| Name | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| Kontext | Kontext | Ja | Gibt den Kontext für die Anfrage an |
| sessionId |  | Zeichenfolge | Nein | Wird zum Verknüpfen mehrerer [!DNL Target] verwendet |
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
| mcId | Zeichenfolge | Nein | Wird zum Zusammenführen und Freigeben von Daten zwischen verschiedenen [!DNL Adobe] (ECID) verwendet. Aus targetCookies abgerufen. Wird automatisch generiert, wenn nicht angegeben. |
| trackingServer | Zeichenfolge | Nein | Der Adobe Analytics-Server, damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen können. |
| trackingServerSecure | Zeichenfolge | Nein | Die [!UICONTROL Adobe Analytics Secure Server], damit [!DNL Adobe Target] und [!DNL Adobe Analytics] die Daten korrekt zusammenfügen können. |
| decisioningMethod | decisioningMethod | Nein | Kann verwendet werden, um die Entscheidungsmethode ON_DEVICE oder HYBRID explizit für On-Device Decisioning festzulegen |

Die Werte der einzelnen Felder sollten *[!UICONTROL Target View Delivery API]* Anfragespezifikation entsprechen. Weitere Informationen zum *[!UICONTROL Target View Delivery API]* finden Sie unter [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Antwort

Die von `TargetClient.getOffers(` zurückgegebene `TargetDeliveryResponse` weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| Anfrage | targetDeliveryRequest&#x200B; | Anfrage *[!DNL Target]* |
| Antwort | deliveryResponse | *[!DNL Target]* Antwort |
| Cookies | Liste | Liste der Sitzungsmetadaten für diesen Benutzer. Muss in der nächsten Target-Anfrage für diesen Benutzer übergeben werden. |
| visitorState | Landkarte | Besucherstatus, der Client-seitig zur Verwendung durch die Besucher-API festgelegt wird |
| responseStatus | ResponseStatus | Ein Objekt, das den Status der Antwort darstellt |

Die `ResponseStatus` in der Antwort enthält die folgenden Felder:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| status | int | HTTP-Status von [!DNL Target] zurückgegeben |
| message | Zeichenfolge | Statusmeldung, falls der HTTP-Status nicht 200 ist |
| remoteMboxes | Liste der Zeichenfolgen | Wird für die geräteinterne Entscheidungsfindung verwendet. Enthält eine Liste der Mboxes mit Remote-Aktivitäten, über die nicht vollständig auf dem Gerät entschieden werden kann. |
| remoteViews | Liste der Zeichenfolgen | Wird für die geräteinterne Entscheidungsfindung verwendet. Enthält eine Liste von Ansichten mit Remote-Aktivitäten, über die nicht vollständig auf dem Gerät entschieden werden kann. |

Das `TargetCookie` -Objekt, das zum Speichern von Daten für Benutzersitzungen verwendet wird, weist die folgende Struktur auf:

| Name | Typ | Beschreibung |
| --- | --- | --- |
| name | Zeichenfolge | Cookie-Name |
| value | Zeichenfolge | Cookie-Wert, der Wert wird in eine Zeichenfolge konvertiert |
| maxAge | Nummer | Die Option maxAge ist eine praktische Methode, um festzulegen, dass die Gültigkeit in Sekunden relativ zur aktuellen Zeit abläuft |

Sie müssen sich keine Sorgen machen, dass die Cookies ablaufen. Target verwaltet maxAge innerhalb der SDK.

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
