---
title: Echtzeit-Profilsynchronisierung für mbox3rdPartyId
description: Erfahren Sie, wie Sie mbox3rdPartyId mit dem  [!DNL Adobe Experience Platform Web SDK].
keywords: Personalisierung;Target;Adobe Target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
source-git-commit: 27759841c8d6a4ac4cc72e735f1dc6512c71aea5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 16%

---

# Was ist mbox3rdPartyId

Die `mbox3rdPartyId` in [!DNL Adobe Target] ist die Besucher-ID Ihres Unternehmens, wie z. B. die Mitgliedschafts-ID des Treueprogramms Ihres Unternehmens.

Wenn sich ein Besucher auf der Website eines Unternehmens anmeldet, erstellt das Unternehmen in der Regel eine ID, die mit dem Konto, der Treuekarte, der Mitgliedschaftsnummer oder anderen Kennungen des Besuchers für dieses Unternehmen verknüpft ist. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=de#)

## Verwendung von `mbox3rdPartyId` mit dem [!DNL Platform Web SDK]

### Schritt 1: Konfigurieren des `Target Third Party ID Namespace`

Konfigurieren Sie die `Target Third Party ID Namespace` in Ihrem [Datenstrom](https://experienceleague.adobe.com/de/docs/experience-platform/datastreams/overview) unter Verwendung des ID-Namespace, den Sie als mbox-Drittanbieter-ID verwenden möchten. [Weitere Informationen zu ID-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)

![Experience Platform-Benutzeroberfläche mit dem Namespace-Feld für die Target-Third-Party-ID.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### Schritt 2: `mbox3rdpartyId` an [!DNL Target] senden

Senden Sie die `mbox3rdpartyId` an [!DNL Target] im `sendEvent`-Befehl unter Verwendung des ID-Namespace, den Sie in Schritt 1 konfiguriert haben.
[Weitere Informationen zum Senden von IDs](../../identity/overview.md#syncing-identities)

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
