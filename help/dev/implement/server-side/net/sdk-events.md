---
title: Abonnieren Sie Ereignisse im [!DNL Adobe Target] .NET SDK
description: Erfahren Sie, wie Sie mithilfe des [!UICONTROL OnDeviceDecisioningHandler] -Objekt.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# SDK-Ereignisse (.NET)

## Beschreibung

Wann [Initialisieren des SDK](initialize-sdk.md), ein optionales `OnDeviceDecisioningReady` delegate kann auf der `TargetClientConfig` -Objekt, das aufgerufen wird, wenn das SDK für On-Device-Methodenaufrufe bereit ist. Es stehen auch einige weitere Delegierte zur Verfügung, die die [!UICONTROL on-device decisioning] Artefakt herunterladen.

## Ereignis- 

Die folgenden Delegate können für bestimmte Ereignisse konfiguriert werden:

| Name | Argumente | Beschreibung |
| --- | --- | --- |
| OnDeviceDecisioningReady | Keine | Wird nur einmal aufgerufen, wenn der Client zum ersten Mal bereit ist für [!UICONTROL on-device decisioning] |
| ArtifactDownloadSucceeded | Zeichenfolgeninhalt der Artefaktdatei | Jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning] Artefakt heruntergeladen |
| ArtifactDownloadFailed | Ausnahme | Jedes Mal aufgerufen, wenn der Download eines [!UICONTROL on-device decisioning] Artefakt |

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
