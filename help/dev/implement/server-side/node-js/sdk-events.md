---
title: Abonnieren von Ereignissen in der [!DNL Adobe Target] Node.js-SDK
description: Erfahren Sie, wie Sie verschiedene Ereignisse in der Node.js-SDK mit dem [!UICONTROL OnDeviceDecisioningHandler]-Objekt abonnieren.
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
TQID: 'https://experienceleague.adobe.com/KWuJT-p-Er-1mx766Y-itlFn7REZnqkUksdHKCy-2-U'
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
source-wordcount: '165'
ht-degree: 2%
---
# SDK-Ereignisse (Node.js)

## Beschreibung

Beim [Initialisieren der SDK](initialize-sdk.md) ist das `options.events`-Objekt ein optionales Objekt mit Ereignisnamenschlüsseln und Rückruffunktionswerten. Sie kann verwendet werden, um verschiedene Ereignisse zu abonnieren, die innerhalb der SDK auftreten. Beispielsweise kann das `clientReady`-Ereignis mit einer Rückruffunktion verwendet werden, die aufgerufen wird, wenn die SDK für Methodenaufrufe bereit ist.

Wenn die Rückruffunktion aufgerufen wird, wird ein Ereignisobjekt übergeben. Jedes Ereignis verfügt über einen `type`, der dem Ereignisnamen entspricht. Einige Ereignisse enthalten zusätzliche Eigenschaften mit relevanten Informationen.

## Ereignis-

| Ereignisname (Typ) | Beschreibung | Zusätzliche Ereigniseigenschaften |
| --- | --- | --- |
| clientReady | Wird ausgegeben, wenn das Artefakt heruntergeladen wurde und die SDK für `getOffers` Aufrufe bereit ist. Wird bei Verwendung der geräteinternen Entscheidungsmethode empfohlen. |  |
| artifactDownload erfolgreich | Wird bei jedem Herunterladen eines neuen Artefakts ausgegeben. | artifactPayload, artifactLocation |
| artifactDownload fehlgeschlagen | Wird jedes Mal ausgegeben, wenn ein Artefakt nicht heruntergeladen werden kann. | artifactLocation, Fehler |

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
