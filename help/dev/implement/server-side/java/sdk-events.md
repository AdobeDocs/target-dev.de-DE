---
title: Abonnieren von Ereignissen in der  [!DNL Adobe Target] -Java-SDK
description: Erfahren Sie, wie Sie mithilfe des [!UICONTROL OnDeviceDecisioningHandler]-Objekts verschiedene Ereignisse abonnieren, die in der Java-SDK auftreten.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# SDK-Ereignisse (Java)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) kann ein optionales `OnDeviceDecisioningHandler`-Objekt für das `ClientConfig` bereitgestellt werden. Sie kann verwendet werden, um verschiedene Ereignisse zu abonnieren, die innerhalb der SDK auftreten. Beispielsweise kann das `onDeviceDecisioningReady`-Ereignis mit einer Rückruffunktion verwendet werden, die aufgerufen wird, wenn die SDK für Methodenaufrufe bereit ist.

## Ereignis- 

Das `OnDeviceDecisioningHandler`-Objekt enthält die folgenden Callbacks, die für bestimmte Ereignisse aufgerufen werden:

| Name | Argumente | Beschreibung |
| --- | --- | --- |
| onDeviceDecisioningReady | Keine | Wird nur aufgerufen, wenn der Client zum ersten Mal [!UICONTROL on-device decisioning] ist |
| artifactDownload erfolgreich | byte[] Inhalt der Artefaktdatei | Wird jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning]-Artefakt heruntergeladen wird |
| artifactDownload fehlgeschlagen | Ausnahme | Wird jedes Mal aufgerufen, wenn ein [!UICONTROL on-device decisioning]-Artefakt nicht heruntergeladen werden kann |

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
