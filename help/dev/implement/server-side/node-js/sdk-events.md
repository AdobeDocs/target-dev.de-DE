---
title: Abonnieren von Ereignissen im SDK [!DNL Adobe Target] Node.js
description: Erfahren Sie, wie Sie mithilfe des Objekts [!UICONTROL OnDeviceDecisioningHandler] verschiedene Ereignisse abonnieren, die im Node.js-SDK auftreten.
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---

# SDK-Ereignisse (Node.js)

## Beschreibung

Beim [ Initialisieren des SDK](initialize-sdk.md) ist das `options.events` -Objekt ein optionales Objekt mit Ereignisnamenschlüsseln und Callback-Funktionswerten. Sie kann zum Abonnieren verschiedener Ereignisse im SDK verwendet werden. Beispielsweise kann das `clientReady` -Ereignis mit einer Callback-Funktion verwendet werden, die aufgerufen wird, wenn das SDK für Methodenaufrufe bereit ist.

Wenn die Rückruffunktion aufgerufen wird, wird ein Ereignisobjekt übergeben. Jedes Ereignis hat einen `type` -Wert, der dem Ereignisnamen entspricht. Einige Ereignisse enthalten zusätzliche Eigenschaften mit relevanten Informationen.

## Ereignis- 

| Ereignisname (Typ) | Beschreibung | Zusätzliche Ereigniseigenschaften |
| --- | --- | --- |
| clientReady | Wird ausgegeben, wenn das Artefakt heruntergeladen wurde und das SDK für `getOffers` -Aufrufe bereit ist. Wird bei Verwendung der Entscheidungsmethode auf dem Gerät empfohlen. |
| artifactDownloadSucceeded | Wird jedes Mal gesendet, wenn ein neues Artefakt heruntergeladen wird. | artifactPayload, artifactLocation |
| artifactDownloadFailed | Wird jedes Mal gesendet, wenn ein Artefakt nicht heruntergeladen werden kann. | artifactLocation, error |

## Beispiel

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
