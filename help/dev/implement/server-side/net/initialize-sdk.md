---
title: Initialisieren des .NET SDK mithilfe der create -Methode
description: Erfahren Sie, wie Sie mit der Methode create das Java SDK initialisieren und die [!UICONTROL TargetClient] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 17%

---

# Initialisieren des .NET SDK

## Beschreibung

Verwenden Sie die `Create` -Methode, um das .NET SDK zu initialisieren und die [!UICONTROL Target-Client] , um [!DNL Adobe Target] für Experimente und personalisierte Erlebnisse.

Bei Verwendung der .NET-Abhängigkeitseingabe fügen Sie einfach das SDK im Dienstkonfigurationsschritt hinzu, indem Sie `services.AddTargetLibrary()`; dann injizieren `ITargetClient targetClient` im Konstruktor Ihrer App verwenden.

Verwenden Sie anschließend die `Initialize` -Methode des SDK verwenden, um das SDK zu konfigurieren und so den Initialisierungsschritt abzuschließen.

## Methode

`TargetClient` wird erstellt mit `TargetClient.Create`.

## C\
#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` wird mit ClientConfig.Builder erstellt.

## C\
#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Parameter

`TargetClientConfig.Builder` weist die folgende Struktur auf:

| Name | Typ | Erforderlich | Standardeinstellung | Beschreibung |
| --- | --- | --- | --- | --- |
| Client- | string | Ja | Keine | [!UICONTROL Target-Client-ID] |
| OrganizationId | string | Ja | Keine | [!UICONTROL Organisations-ID des Experience Cloud] |
| Zeitüberschreitung | int | Nein | 10000 | Zeitüberschreitung für alle Anforderungen in Millisekunden |
| Proxy |  | WebProxy | Nein | null  | Proxy für alle [!DNL Target] requests |
| RetryPolicy | Richtlinie | Nein | null  | Richtlinie für alle wiederholen [!DNL Target] requests |
| AsyncRetryPolicy | AsyncPolicy | Nein | null  | Asynchrone Wiederholungsrichtlinie für alle [!DNL Target] requests |
| Logger | ILogger | Nein | null  | Dient zur Debug-Protokollierung von [!DNL Target] Anforderungen und Antworten |
| ServerDomain | string | Nein | `client.tt.omtrdc.net` | Überschreibt den standardmäßigen Hostnamen |
| Sicher | bool | Nein | wahr | Nicht festgelegt zur Erzwingung des HTTP-Schemas |
| DefaultPropertyToken | string | Nein | null  | Legt das standardmäßige Eigenschafts-Token für jede `getOffers` call |
| TelemetryEnabled | bool | Nein | wahr | Telemetrikdaten zur Verbesserung der SDK-Nutzung senden |
| DecisioningMethod | DecisioningMethod enum | Nein | ServerSide | Muss auf OnDevice oder Hybrid gesetzt sein, um die Entscheidungsfindung auf dem Gerät zu aktivieren |
| OnDeviceDecisioningReady | Aktion | Nein | null  | Für gerätebezogene Entscheidungsfindung delegieren (einmal aufgerufen, wenn die Entscheidung auf dem Gerät fertig ist) |
| ArtifactDownloadSucceeded | Aktion | Nein | null  | Delegieren Sie für den Erfolg des Herunterladens von Artefakten auf dem Gerät (bei jedem erfolgreichen Artefakt-Download aufgerufen). |
| ArtifactDownloadFailed | Aktion | Nein | null  | Delegieren Sie für den Fehler beim Herunterladen von auf dem Gerät befindlichen Entscheidungsartefakten (bei jedem fehlgeschlagenen Artefakt-Download aufgerufen). |
| OnDeviceEnvironment | string | Nein | production | Kann verwendet werden, um eine andere On-Device-Umgebung wie Staging anzugeben |
| OnDeviceConfigHostname | string | Nein | `assets.adobetarget.com` | Kann verwendet werden, um einen anderen Host zum Herunterladen der auf dem Gerät befindlichen Entscheidungsartefaktdatei anzugeben |
| OnDeviceDecisioningPollingIntSecs | int | Nein | 300 (5 Minuten) | Anzahl der Sekunden zwischen Abrufen der auf dem Gerät befindlichen Entscheidungsartefaktdatei |
| OnDeviceArtifactPayload | string | Nein | null  | Bietet On-Device-Entscheidungsfindung mit einer lokalen Artefakt-Payload, um die sofortige Ausführung zu ermöglichen |

## Beispiel

## C\
#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
