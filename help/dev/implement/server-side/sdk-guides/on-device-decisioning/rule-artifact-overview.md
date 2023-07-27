---
title: Grundlegendes zum Entscheidungsregel-Artefakt auf dem Gerät
description: Erfahren Sie, wie Sie das Regel-Artefakt verwenden, das eine JSON-Darstellung Ihrer [!DNL Adobe Target] [!UICONTROL on-device decisioning] Aktivitäten.
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Übersicht über Regelartefakte

Das Regelartefakt ist eine JSON-Darstellung Ihrer [!DNL Adobe Target] [!UICONTROL on-device decisioning] Aktivitäten. Sie wird von [!DNL Adobe Target] und an das Akamai-CDN weitergeleitet werden, um sicherzustellen, dass Ihren Endbenutzern ein Regel-Artefakt so nah wie möglich zur Verfügung steht. Es enthält Metadaten, die die präzise Ausführung und Bereitstellung Ihrer Aktivitäten sicherstellen und gleichzeitig Echtzeitanalysen über das Ereignis-Tracking ermöglichen. Die [!DNL Adobe Target] SDKs können so konfiguriert werden, dass eine automatische Verwaltung des Regelartefakts möglich ist. Damit kann es gemäß einem benutzerdefinierten Zeitintervall heruntergeladen oder aktualisiert werden. Darüber hinaus können Sie Ihre eigene lokale Kopie des Regel-Artefakts mithilfe eines verteilten Speicher-Caching-Systems wie [Memcached](https://memcached.org/) , um die [!DNL Adobe Target] SDK, sodass Ihre stateless-Server Anforderungen sofort bearbeiten können. Weitere Informationen zu diesen Optionen finden Sie in den folgenden Handbüchern:

* [Das automatische Herunterladen, Speichern und Aktualisieren des Regelartefakts über das [!DNL Adobe Target] SDK](rule-artifact-sdk.md)
* [Herunterladen, Speichern und Aktualisieren des Regelartefakts über die JSON-Payload](rule-artifact-json.md)

## Beispielregel-Artefakt

Klicken Sie hier für ein Beispiel der [Regelartefakt](rule-artifact-example.md).

## Anzeigen des Regelartefakts für Ihren Client

Durch das Aktivieren von Traces werden zusätzliche Informationen aus [!DNL Adobe Target] in Bezug auf das Regelartefakt, insbesondere die URL.

1. Navigieren Sie zur Target-Benutzeroberfläche.

   &lt;!— Fügen Sie image-target-ui-1.png —>
   ![ALT-Bild](assets/asset-rule-artifact-1.png)

1. Navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** und klicken **[!UICONTROL Neues Autorisierungstoken generieren]**.

   &lt;!— Fügen Sie image-target-ui-2.png —>
   ![ALT-Bild](assets/asset-rule-artifact-2.png)

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

1. Geben Sie die Zielspur über das Terminal aus, um Details zum Artefakt anzuzeigen. Auf die URL kann über die `artifactLocation` -Variable.

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
