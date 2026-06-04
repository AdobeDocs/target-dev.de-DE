---
title: Echtzeit-Profilsynchronisierung für mbox3rdPartyId
description: Erfahren Sie, wie Sie mbox3rdPartyId mit dem  [!DNL Adobe Experience Platform Web SDK].
keywords: Personalisierung;Target;Adobe Target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
exl-id: 1c5067ef-38b3-4bf1-bd39-ea0f2cbd1074
TQID: https://experienceleague.adobe.com/Ej2sYVnBD9orRTlsMQG85JJV7dvn-9gnABDa0b8uBlM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 35%

---

# mbox3rdPartyId verwenden

Die `mbox3rdPartyId` in [!DNL Adobe Target] ist die Besucher-ID Ihres Unternehmens, wie z. B. die Zugehörigkeits-ID des Treueprogramms Ihres Unternehmens.

Wenn sich ein Besucher bei einer Unternehmenswebsite anmeldet, erstellt das Unternehmen in der Regel eine ID, die seinem Konto, seiner Treuekarte, seiner Mitgliedsnummer oder anderen für das Unternehmen relevanten Identifikatoren zugeordnet wird. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## Verwendung von `mbox3rdPartyId` mit dem [!DNL Platform Web SDK]

### Schritt 1: Konfigurieren des `Target Third Party ID Namespace`

Konfigurieren Sie die `Target Third Party ID Namespace` in Ihrem [Datenstrom](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) unter Verwendung des ID-Namespace, den Sie als mbox-Drittanbieter-ID verwenden möchten. [Weitere Informationen zu ID-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Experience Platform-Benutzeroberfläche mit dem Namespace-Feld für die Target-Third-Party-ID.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Schritt 2: `mbox3rdpartyId` an [!DNL Target] senden

Senden Sie die `mbox3rdpartyId` an [!DNL Target] im `sendEvent`-Befehl unter Verwendung des ID-Namespace, den Sie in Schritt 1 konfiguriert haben.
[Weitere Informationen zum Senden von IDs](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
