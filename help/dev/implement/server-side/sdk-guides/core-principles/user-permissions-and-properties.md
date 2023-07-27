---
title: Benutzerberechtigungen und Eigenschaften
description: Die [!DNL Target] SDKs enthalten Unterstützung für Benutzerberechtigungen und Eigenschaften.
exl-id: 612faf1a-e8f9-4321-b831-90fba69ead3a
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 9%

---

# Benutzerberechtigungen und Eigenschaften

Die [!DNL Target] SDKs enthalten Unterstützung für Benutzerberechtigungen und Eigenschaften. Wenn Sie nicht genau wissen, wie [!DNL Adobe Target] verarbeitet Unternehmensberechtigungen über Arbeitsbereiche und Eigenschaften. Weitere Informationen dazu finden Sie unter [Berechtigungen für Unternehmensbenutzer](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de).

Der Client kann ein Eigenschafts-Token auf zwei Arten verwenden.

## Globales Eigenschafts-Token

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    propertyToken: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({...})
```

>[!TAB Java ]

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("emeaprod4")
    .organizationId("0DD934B85278256B0A490D44@AdobeOrg")
    .defaultPropertyToken("8c4630b1-16db-e2fc-3391-8b3d81436cfb")
    .build();

TargetClient targetClient = TargetClient.create(clientConfig);
```

>[!ENDTABS]

## Incident Property Token im getOffers-Aufruf

Ein Eigenschafts-Token kann auch in einem einzelnen `getOffers` aufrufen. Dazu fügen Sie der Anforderung ein Eigenschaftsobjekt hinzu. Ein auf diese Weise angegebenes Eigenschafts-Token hat Vorrang vor einem Satz in der Konfiguration.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
    request: {
        execute: {
            pageLoad: {}
        },
        property: {
            token: "8c4630b1-16db-e2fc-3391-8b3d81436cfb"
        }           
    }
})
```

>[!TAB Java ]

```java {line-numbers="true"}
ExecuteRequest executeRequest = new ExecuteRequest()
    .mboxes(getMboxRequests(mbox));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
    .context(getContext(request))
    .execute(executeRequest)
    .cookies(getTargetCookies(request.getCookies()))
    .property(new Property().token("8c4630b1-16db-e2fc-3391-8b3d81436cfb"))
    .build();

TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
```

>[!ENDTABS]
