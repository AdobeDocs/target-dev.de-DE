---
title: Initialisieren des Java-SDK mit der create-Methode
description: Erfahren Sie, wie Sie die Methode create verwenden, um das Java-SDK zu initialisieren und die [!UICONTROL TargetClient] zu instanziieren, um für Experimente und personalisierte Erlebnisse Aufrufe an  [!DNL Adobe Target]  durchzuführen.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 17%

---

# Initialisieren des Java-SDK

## Beschreibung

Verwenden Sie die `create` -Methode, um das Java-SDK zu initialisieren und die [!UICONTROL Target Client] zu instanziieren, um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse aufzurufen.

## Methode

[!UICONTROL TargetClient] wird mit `TargetClient.create` erstellt.

### erstellen

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig wird mit `ClientConfig.builder` erstellt.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parameter

`ClientConfigBuilder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| client | Zeichenfolge | Ja | Keine | [!UICONTROL Target Client Id] |
| organizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Experience Cloud Organization ID] |
| connectTimeout | Nummer | Nein | 10000 | Zeitüberschreitung bei der Verbindung für alle Anforderungen in Millisekunden |
| socketTimeout | Nummer | Nein | 10000 | Socket-Timeout für alle Anforderungen in Millisekunden |
| maxConnectionsPerHost | Nummer | Nein | 100 | Max. Verbindungen pro [!DNL Target] Host |
| maxConnectionsTotal | Nummer | Nein | 200 | Max. Verbindungen einschließlich aller [!DNL Target] Hosts |
| connectionTlFrau | Nummer | Nein | -1 | &quot;Gesamte Lebensdauer&quot;(TTL) definiert die maximale Lebensdauer persistenter Verbindungen in Millisekunden. Standardmäßig bleiben Verbindungen unbegrenzt aktiv |
| idleConnectionValidationMS | Nummer | Nein | 1000 | Inaktivitätszeitraum in Millisekunden, nach dem persistente Verbindungen vor der Wiederverwendung erneut validiert werden |
| evictIdleConnectionsAfterSecs | Nummer | Nein | 20 | Die Zeit in Sekunden, um inaktive Verbindungen aus dem Verbindungspool zu entfernen. |
| enableRetries | Boolesch | Nein | wahr | Automatische Wiederholungen für Socket-Timeouts (max. 4) |
| logRequests | Boolesch | Nein | false | Log [!DNL Target] requests and responses in debug |
| logRequestStatus | Boolesch | Nein | false | Log [!DNL Target] response time, status and URL |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den standardmäßigen Hostnamen |
| secure | Boolesch | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| requestInterceptor | HttpRequestInterceptor | Nein | Null | Benutzerdefinierten Anforderungsauslöser hinzufügen |
| defaultPropertyToken | Zeichenfolge | Nein | Keine | Legt das standardmäßige Eigenschafts-Token für jeden `getOffers` -Aufruf fest. **Für Entscheidungen auf dem Gerät** lädt das SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschaft-Token enthält, das in `defaultPropertyToken` festgelegt ist. |
| defaultDecisioningMethod | DecisioningMethod enum | Nein | SERVER_SIDE | Muss auf ON_DEVICE oder HYBRID gesetzt werden, um die Entscheidungsfindung auf dem Gerät zu ermöglichen |
| telemetryEnabled | Boolesch | Nein | wahr | Ermöglicht Kunden, die zusätzliche Datenerfassung bei Anfragen an [!DNL Target] -Server abzulehnen |
| proxyConfig | ClientProxyConfig | Nein | Keine | Ermöglicht es dem Client, eigene Proxy-Details anzugeben |
| exceptionHandler | TargetExceptionHandler | Nein | Keine | Kann zur Implementierung der benutzerdefinierten Ausnahmebehandlung während der Regelverarbeitung verwendet werden |
| httpClient | HttpClient | Nein | Keine | Ermöglicht Benutzern, den HTTP-Client [!DNL Target] durch einen benutzerdefinierten HTTP-Client zu ersetzen |
| onDeviceEnvironment | Zeichenfolge | Nein | production | Kann verwendet werden, um eine andere On-Device-Umgebung anzugeben, z. B. Staging |
| onDeviceConfigHostname | Zeichenfolge | Nein | `assets.adobetarget.com` | Kann verwendet werden, um einen anderen Host zum Herunterladen der auf dem Gerät befindlichen Entscheidungsartefaktdatei anzugeben |
| onDeviceDecisioningPollingIntSecs | int | Nein | 300 (5 Minuten) | Anzahl der Sekunden zwischen Abrufen der auf dem Gerät befindlichen Entscheidungsartefaktdatei |
| onDeviceArtifactPayload | byte[] | Nein | Keine | Bietet eine geräteübergreifende Entscheidungsfindung mit vorheriger Artefakt-Payload, um eine sofortige Ausführung zu ermöglichen |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Nein | Keine | Registriert Callbacks für on-device-Entscheidungsereignisse |
| onDeviceAllMatchingRulesMboxes | List\&lt;String\> | Nein | Keine | Ermöglicht Benutzern, Mboxes anzugeben, für die bei der geräteübergreifenden Entscheidung der gesamte übereinstimmende Regelinhalt zurückgegeben wird |

## Beispiel

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
