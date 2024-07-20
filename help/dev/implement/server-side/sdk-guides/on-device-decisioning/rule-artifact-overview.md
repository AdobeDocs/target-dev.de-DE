---
title: Grundlegendes zum Entscheidungsregel-Artefakt auf dem Gerät
description: Erfahren Sie, wie Sie das Regel-Artefakt verwenden, das eine JSON-Darstellung Ihrer [!DNL Adobe Target] [!UICONTROL on-device decisioning] -Aktivitäten ist.
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Übersicht über Regelartefakte

Das Regelartefakt ist eine JSON-Darstellung Ihrer [!DNL Adobe Target] [!UICONTROL on-device decisioning] -Aktivitäten. Sie wird von [!DNL Adobe Target] generiert und an das Akamai-CDN weitergeleitet, um sicherzustellen, dass Ihren Endbenutzern ein Regel-Artefakt so nah wie möglich zur Verfügung steht. Es enthält Metadaten, die die präzise Ausführung und Bereitstellung Ihrer Aktivitäten sicherstellen und gleichzeitig Echtzeitanalysen über das Ereignis-Tracking ermöglichen. Die [!DNL Adobe Target] -SDKs können so konfiguriert werden, dass sie eine automatische Verwaltung des Regelartefakts ermöglichen, sodass es gemäß einem benutzerdefinierten Zeitintervall heruntergeladen oder aktualisiert werden kann. Darüber hinaus können Sie Ihre eigene lokale Kopie des Regelartefakts mithilfe eines dezentralen Speicherzwischenspeichersystems wie [Memcached](https://memcached.org/) verwalten, um das [!DNL Adobe Target]-SDK zu initialisieren, sodass Ihre statuslosen Server Anfragen sofort bedienen können. Weitere Informationen zu diesen Optionen finden Sie in den folgenden Handbüchern:

* [Herunterladen, Speichern und Aktualisieren des Regelartefakts automatisch über das [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Herunterladen, Speichern und Aktualisieren des Regelartefakts über die JSON-Payload](rule-artifact-json.md)

## Beispielregel-Artefakt

Klicken Sie hier für ein Beispiel des [Regel-Artefakts](rule-artifact-example.md).

## Anzeigen des Regelartefakts für Ihren Client

Durch das Aktivieren von Traces werden zusätzliche Informationen von [!DNL Adobe Target] in Bezug auf das Regel-Artefakt, insbesondere die URL, ausgegeben.

1. Navigieren Sie zur Target-Benutzeroberfläche.

   &lt;!— Fügen Sie image-target-ui-1.png —>
   ![alt image](assets/asset-rule-artifact-1.png)

1. Navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** und klicken Sie auf **[!UICONTROL Generate New Authorization Token]**.

   &lt;!— Fügen Sie image-target-ui-2.png —>
   ![alt image](assets/asset-rule-artifact-2.png)

1. Kopieren Sie das neu generierte Autorisierungstoken in die Zwischenablage und fügen Sie es zu Ihrer Target-Anfrage hinzu.

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. Geben Sie die Zielspur über das Terminal aus, um Details zum Artefakt anzuzeigen. Auf die URL kann über die Variable `artifactLocation` zugegriffen werden.

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
