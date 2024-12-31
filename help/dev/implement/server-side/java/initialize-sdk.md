---
title: Initialisieren Sie die Java-SDK mit der create-Methode
description: Erfahren Sie, wie Sie mit der create-Methode die Java-SDK initialisieren und die [!UICONTROL TargetClient] instanziieren können, um  [!DNL Adobe Target]  für Experimente und personalisierte Erlebnisse aufzurufen.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 17%

---

# Initialisieren der Java-SDK

## Beschreibung

Verwenden Sie die `create`-Methode, um die Java-SDK zu initialisieren und die [!UICONTROL Target Client] zu instanziieren und [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse aufzurufen.

## Methode

[!UICONTROL TargetClient] wird mithilfe von `TargetClient.create` erstellt.

### erstellen

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig wird mithilfe von `ClientConfig.builder` erstellt.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parameter

`ClientConfigBuilder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Kunde | Zeichenfolge | Ja | Keine | [!UICONTROL Target Client Id] |
| OrganizationId | Zeichenfolge | Ja | Keine | [!UICONTROL Experience Cloud Organization ID] |
| connectTimeout | Nummer | Nein | 10000 | Verbindungs-Timeout für alle Anfragen in Millisekunden |
| socketTimeout | Nummer | Nein | 10000 | Socket-Zeitüberschreitung für alle Anfragen in Millisekunden |
| maxConnectionsPerHost | Nummer | Nein | 100 | Max. Verbindungen pro [!DNL Target] |
| maxConnectionsTotal | Nummer | Nein | 200 | Max. Verbindungen, einschließlich aller [!DNL Target] Hosts |
| connectionTTLms | Nummer | Nein | -1 | Die TTL (Total Time to Live) definiert die maximale Lebensdauer persistenter Verbindungen in Millisekunden. Standardmäßig werden Verbindungen auf unbestimmte Zeit aufrechterhalten |
| idleConnectionValidationMs | Nummer | Nein | 1000 | Inaktivitätsdauer in Millisekunden, nach deren Ablauf persistente Verbindungen vor der Wiederverwendung erneut validiert werden |
| evictIdleConnectionsAfterSecs | Nummer | Nein | 20 | Die Zeit in Sekunden, die inaktive Verbindungen aus dem Verbindungspool entfernt werden sollen |
| enableRetries | Boolesch | Nein | wahr | Automatische Wiederholungen für Socket-Timeouts (max. 4) |
| logRequests | Boolesch | Nein | false | [!DNL Target] Anfragen und Antworten in Debug protokollieren |
| logRequestStatus | Boolesch | Nein | false | [!DNL Target] Reaktionszeit, Status und URL protokollieren |
| serverDomain | Zeichenfolge | Nein | `*client*.tt.omtrdc.net` | Überschreibt den Standard-Host-Namen |
| sicher | Boolesch | Nein | wahr | Einstellung zur Durchsetzung des HTTP-Schemas |
| RequestInterceptor | HttpRequestInterceptor | Nein | Null | Hinzufügen eines benutzerdefinierten Anforderungs-Interceptors |
| defaultPropertyToken | Zeichenfolge | Nein | Keine | Legt das standardmäßige Eigenschafts-Token für jeden `getOffers` fest. **Bei der geräteinternen** lädt die SDK nur das Artefakt herunter, das die qualifizierten Aktivitäten für das Eigenschaften-Token enthält, das in festgelegt `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod-Enumeration | Nein | SERVER_SIDE | Muss auf ON_DEVICE oder HYBRID festgelegt werden, um On-Device Decisioning zu aktivieren |
| telemetrisch aktiviert | Boolesch | Nein | wahr | Ermöglicht es Kunden, die zusätzliche Datenerfassung bei Anfragen an [!DNL Target] Server abzuwählen |
| proxyConfig | ClientProxyConfig | Nein | Keine | Ermöglicht dem Client, seine eigenen Proxy-Details anzugeben |
| exceptionHandler | TargetExceptionHandler | Nein | Keine | Kann verwendet werden, um während der Regelverarbeitung die benutzerdefinierte Ausnahmebehandlung zu implementieren |
| httpClient | HttpClient | Nein | Keine | Ermöglicht Benutzern, den [!DNL Target] HTTP-Client durch einen benutzerdefinierten HTTP-Client zu ersetzen |
| onDeviceEnvironment | Zeichenfolge | Nein | Produktion | Kann verwendet werden, um eine andere On-Device-Umgebung anzugeben, z. B. Staging |
| onDeviceConfigHost-Name | Zeichenfolge | Nein | `assets.adobetarget.com` | Kann verwendet werden, um einen anderen Host zum Herunterladen der Artefaktdatei für die geräteinterne Entscheidungsfindung anzugeben |
| onDeviceDecisioningPollingIntSecs | int | Nein | 300 (5 Minuten) | Anzahl der Sekunden zwischen den Abrufen der Artefaktdatei für die geräteinterne Entscheidungsfindung |
| onDeviceArtifactPayload | byte[] | Nein | Keine | Bietet Entscheidungsfindung auf dem Gerät mit vorheriger Artefakt-Payload, um die sofortige Ausführung zu ermöglichen |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Nein | Keine | Registriert Callbacks für On-Device Decisioning-Ereignisse |
| onDeviceAllMatchingRulesMboxes | list\&lt;string\> | Nein | Keine | Ermöglicht es Benutzenden, Mboxes anzugeben, für die alle übereinstimmenden Regelinhalte während der geräteinternen Entscheidungsfindung zurückgegeben werden |

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
