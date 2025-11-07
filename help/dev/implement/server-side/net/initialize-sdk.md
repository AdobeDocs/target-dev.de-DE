---
title: Initialisieren von .NET SDK mithilfe der create-Methode
description: Erfahren Sie, wie Sie mit der create-Methode die Java-SDK initialisieren und die [!UICONTROL TargetClient] instanziieren können, um  [!DNL Adobe Target]  für Experimente und personalisierte Erlebnisse aufzurufen.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 16%

---

# Initialisieren von .NET SDK

## Beschreibung

Verwenden Sie die `Create`-Methode, um .NET SDK zu initialisieren und die [!UICONTROL Target Client] zu instanziieren und [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse aufzurufen.

Fügen Sie bei Verwendung von .NET Dependency Injection einfach den Konfigurationsschritt SDK at service hinzu, indem Sie `services.AddTargetLibrary()`; aufrufen, und fügen Sie dann `ITargetClient targetClient` in den Konstruktor Ihrer App ein.

Verwenden Sie danach die `Initialize`-Methode von SDK, um die SDK zu konfigurieren, und schließen Sie so den Initialisierungsschritt ab.

## Methode

`TargetClient` wird mithilfe von `TargetClient.Create` erstellt.

## C\#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` wird mit ClientConfig.Builder erstellt.

## C\#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parameter

`TargetClientConfig.Builder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Client | string | Ja | Keine | [!UICONTROL Target Client Id] |
| OrganizationId | string | Ja | Keine | [!UICONTROL Experience Cloud Organization ID] |
| Zeitüberschreitung | int | Nein | 10000 | Zeitüberschreitung für alle Anforderungen in Millisekunden |
| Proxy | WebProxy | Nein | null  | Proxy für alle [!DNL Target] |
| Richtlinie wiederholen | Richtlinie | Nein | null  | Richtlinie für alle [!DNL Target] wiederholen |
| AsyncRetryPolicy | AsyncPolicy | Nein | null  | Asynchrone Wiederholungsrichtlinie für alle [!DNL Target] |
| Logger | ILogger | Nein | null  | Wird für die Debug-Protokollierung von [!DNL Target] und Antworten verwendet |
| ServerDomain | string | Nein | `client.tt.omtrdc.net` | Überschreibt den Standard-Host-Namen |
| Sicher | boolesch | Nein | wahr | Einstellung zur Durchsetzung des HTTP-Schemas |
| DefaultPropertyToken | string | Nein | null  | Legt das standardmäßige Eigenschafts-Token für jeden `getOffers` fest |
| Telemetrie aktiviert | boolesch | Nein | wahr | Senden von Telemetriedaten zur Verbesserung der SDK-Nutzung |
| decisioningMethod | DecisioningMethod-Enumeration | Nein | Server-seitig | Muss auf „OnDevice“ oder „Hybrid“ festgelegt werden, um die geräteinterne Entscheidungsfindung zu aktivieren |
| OnDeviceDecisioningReady | Aktion | Nein | null  | Delegieren des Ereignisses „Bereit für On-Device Decisioning“ (wird einmal aufgerufen, wenn die On-Device Decisioning bereit ist) |
| Artefakt-Download erfolgreich | Aktion | Nein | null  | Delegieren für „Artefakt-Download auf dem Gerät“ (wird bei jedem erfolgreichen Artefakt-Download aufgerufen) |
| artifactDownload fehlgeschlagen | Aktion | Nein | null  | Delegieren für Fehler beim Herunterladen von Artefakten auf dem Gerät beim Decisioning (wird bei jedem fehlgeschlagenen Artefakt-Download aufgerufen) |
| OnDeviceEnvironment | string | Nein | Produktion | Kann verwendet werden, um eine andere On-Device-Umgebung wie Staging anzugeben |
| OnDeviceConfigHost-Name | string | Nein | `assets.adobetarget.com` | Kann verwendet werden, um einen anderen Host zum Herunterladen der Artefaktdatei für die geräteinterne Entscheidungsfindung anzugeben |
| OnDeviceDecisioningPollingIntSecs | int | Nein | 300 (5 min) | Anzahl der Sekunden zwischen den Abrufen der Artefaktdatei für die geräteinterne Entscheidungsfindung |
| OnDeviceArtifactPayload | string | Nein | null  | Bietet geräteinterne Entscheidungsfindung mit einer lokalen Artefakt-Payload, um die sofortige Ausführung zu ermöglichen |

## Beispiel

## C\#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
