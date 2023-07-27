---
title: Abonnieren Sie Ereignisse im [!DNL Adobe Target] Java-SDK
description: Erfahren Sie, wie Sie mithilfe der Variablen [!UICONTROL OnDeviceDecisioningHandler] -Objekt.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 4%

---

# SDK-Ereignisse (Java)

## Beschreibung

Wann [Initialisieren des SDK](initialize-sdk.md), ein optionales `OnDeviceDecisioningHandler` -Objekt kann auf der `ClientConfig` -Objekt. Sie kann zum Abonnieren verschiedener Ereignisse im SDK verwendet werden. Beispielsweise wird die `onDeviceDecisioningReady` -Ereignis kann mit einer Callback-Funktion verwendet werden, die aufgerufen wird, wenn das SDK für Methodenaufrufe bereit ist.

## Ereignis- 

Die `OnDeviceDecisioningHandler` -Objekt enthält die folgenden Rückrufe, die für bestimmte Ereignisse aufgerufen werden:

| Name | Argumente | Beschreibung |
| --- | --- | --- |
| onDeviceDecisioningReady | Keine | Wird nur einmal aufgerufen, wenn der Client zum ersten Mal bereit ist für [!UICONTROL on-device decisioning] |
| artifactDownloadSucceeded | byte[] Inhalt der Artefaktdatei | Jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning] Artefakt heruntergeladen |
| artifactDownloadFailed | Ausnahme | Jedes Mal aufgerufen, wenn der Download einer [!UICONTROL on-device decisioning] Artefakt |

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
