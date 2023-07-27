---
title: Initialisieren des Java-SDK mit der create-Methode
description: Erfahren Sie, wie Sie mit der Methode create das Java SDK initialisieren und die [!UICONTROL TargetClient] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 18%

---

# Initialisieren des Java-SDK

## Beschreibung

Verwenden Sie die `create` -Methode verwenden, um das Java-SDK zu initialisieren und die [!UICONTROL Target-Client] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.

## Methode

[!UICONTROL TargetClient] wird erstellt mit `TargetClient.create`.

### erstellen

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig wird mithilfe von `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parameter

`ClientConfigBuilder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| client | Zeichenfolge | Ja | Keine | [!UICONTROL Target-Client-ID] |
| organizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Organisations-ID des Experience Cloud] |
| connectTimeout | Nummer | Nein | 10000 | Zeitüberschreitung bei der Verbindung für alle Anforderungen in Millisekunden |
| socketTimeout | Nummer | Nein | 10000 | Socket-Timeout für alle Anforderungen in Millisekunden |
| maxConnectionsPerHost | Nummer | Nein | 100 | Max. Verbindungen pro [!DNL Target] Host |
| maxConnectionsTotal | Nummer | Nein | 200 | Max. Verbindungen einschließlich aller [!DNL Target] hosts |
| enableRetries | Boolesch | Nein | wahr | Automatische Wiederholungen für Socket-Timeouts (max. 4) |
| logRequests | Boolesch | Nein | false | Protokoll [!DNL Target] Anforderungen und Antworten im Debugging |
| logRequestStatus | Boolesch | Nein | false | Protokoll [!DNL Target] Antwortzeit, Status und URL |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den standardmäßigen Hostnamen |
| secure | Boolesch | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| requestInterceptor | HttpRequestInterceptor | Nein | Null | Benutzerdefinierten Anforderungsauslöser hinzufügen |
| defaultPropertyToken | Zeichenfolge | Nein | Keine | Legt das standardmäßige Eigenschafts-Token für jede `getOffers` aufrufen. **Für geräteübergreifende Entscheidungen**, lädt das SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschafts-Token enthält, das in `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod enum | Nein | SERVER_SIDE | Muss auf ON_DEVICE oder HYBRID gesetzt werden, um die Entscheidungsfindung auf dem Gerät zu ermöglichen |
| telemetryEnabled | Boolesch | Nein | wahr | Ermöglicht Kunden, die zusätzliche Datenerfassung bei Anfragen an abzuwählen. [!DNL Target] Server |
| proxyConfig | ClientProxyConfig | Nein | Keine | Ermöglicht es dem Client, eigene Proxy-Details anzugeben |
| exceptionHandler | TargetExceptionHandler | Nein | Keine | Kann zur Implementierung der benutzerdefinierten Ausnahmebehandlung während der Regelverarbeitung verwendet werden |
| httpClient | HttpClient | Nein | Keine | Ermöglicht Benutzern, die [!DNL Target] HTTP-Client mit benutzerdefiniertem HTTP-Client |
| onDeviceEnvironment | Zeichenfolge | Nein | production | Kann verwendet werden, um eine andere On-Device-Umgebung anzugeben, z. B. Staging |
| onDeviceConfigHostname | Zeichenfolge | Nein | `assets.adobetarget.com` | Kann verwendet werden, um einen anderen Host zum Herunterladen der auf dem Gerät befindlichen Entscheidungsartefaktdatei anzugeben |
| onDeviceDecisioningPollingIntSecs | int | Nein | 300 (5 Minuten) | Anzahl der Sekunden zwischen Abrufen der auf dem Gerät befindlichen Entscheidungsartefaktdatei |
| onDeviceArtifactPayload | Byte[] | Nein | Keine | Bietet eine geräteübergreifende Entscheidungsfindung mit vorheriger Artefakt-Payload, um eine sofortige Ausführung zu ermöglichen |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Nein | Keine | Registriert Callbacks für on-device-Entscheidungsereignisse |
| onDeviceAllMatchingRulesMboxes | Liste\&lt;string> | Nein | Keine | Ermöglicht Benutzern, Mboxes anzugeben, für die bei der geräteübergreifenden Entscheidung der gesamte übereinstimmende Regelinhalt zurückgegeben wird |

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
