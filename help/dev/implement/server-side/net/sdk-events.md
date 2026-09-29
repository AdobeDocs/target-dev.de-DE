---
title: Abonnieren von Ereignissen in [!DNL Adobe Target] .NET SDK
description: Erfahren Sie, wie Sie verschiedene Ereignisse in .NET SDK mit dem [!UICONTROL OnDeviceDecisioningHandler]-Objekt abonnieren.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: 'https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%
---
# SDK-Ereignisse (.NET)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) kann ein optionaler `OnDeviceDecisioningReady`-Delegat für das `TargetClientConfig`-Objekt bereitgestellt werden, der aufgerufen wird, wenn die SDK für Methodenaufrufe auf dem Gerät bereit ist. Es gibt auch einige andere Delegaten, die für die Handhabung des [!UICONTROL On-Device Decisioning]-Artefakts-Downloads verfügbar sind.

## Ereignis-

Die folgenden Delegaten können für bestimmte Ereignisse konfiguriert werden:

| Name | Argumente | Beschreibung |
| --- | --- | --- |
| OnDeviceDecisioningReady | Keine | Wird nur aufgerufen, wenn der Client zum ersten Mal für die [!UICONTROL -On-Device Decisioning bereit ist] |
| Artefakt-Download erfolgreich | Zeichenfolgeninhalte der Artefaktdatei | Wird jedes Mal aufgerufen, wenn ein [!UICONTROL On-Device Decisioning]-Artefakt heruntergeladen wird |
| artifactDownload fehlgeschlagen | Ausnahme | Wird jedes Mal aufgerufen, wenn ein Fehler beim Herunterladen eines [!UICONTROL On-Device Decisioning“-] auftritt |

## Beispiel

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
