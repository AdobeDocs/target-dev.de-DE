---
title: Abonnieren von Ereignissen im  [!DNL Adobe Target] Java-SDK
description: Erfahren Sie, wie Sie mithilfe des Objekts [!UICONTROL OnDeviceDecisioningHandler] verschiedene Ereignisse abonnieren, die im Java-SDK auftreten.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# SDK-Ereignisse (Java)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) kann ein optionales `OnDeviceDecisioningHandler` -Objekt für das `ClientConfig` -Objekt bereitgestellt werden. Sie kann zum Abonnieren verschiedener Ereignisse im SDK verwendet werden. Beispielsweise kann das `onDeviceDecisioningReady` -Ereignis mit einer Callback-Funktion verwendet werden, die aufgerufen wird, wenn das SDK für Methodenaufrufe bereit ist.

## Ereignis- 

Das Objekt `OnDeviceDecisioningHandler` enthält die folgenden Rückrufe, die für bestimmte Ereignisse aufgerufen werden:

| Name | Argumente | Beschreibung |
| --- | --- | --- |
| onDeviceDecisioningReady | Keine | Wird nur einmal aufgerufen, wenn der Client zum ersten Mal für [!UICONTROL on-device decisioning] bereit ist |
| artifactDownloadSucceeded | byte[] content of artifact file | Wird jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning] -Artefakt heruntergeladen wird |
| artifactDownloadFailed | Ausnahme | Jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning] -Artefakt nicht heruntergeladen werden kann |

## Beispiel

### SDK-Ereignisse

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
