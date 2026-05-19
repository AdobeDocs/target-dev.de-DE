---
title: Protokollierung von Adobe Analytics for Target (A4T) in der Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Erfassung von Daten aus Adobe Analytics for Target (A4T) mit der Experience Platform Web SDK steuern.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;Protokollierung;Analytics;SDK;Web SDK;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# [!DNL Adobe Analytics for Target] (A4T)-Protokollierung in der [!DNL Experience Platform Web SDK]

Bei der Verwendung von [!DNL Adobe Target] für die Personalisierung können Sie auswählen, welches System Sie für die Leistungsmessung verwenden möchten. Jede [Target-Aktivität](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de) ermöglicht die Auswahl zwischen [!DNL Target] Reporting und Adobe [!DNL Analytics] Reporting.

Wenn Sie [!DNL Analytics] Reporting verwenden, müssen [!DNL Target] den [!DNL Analytics] Folgendes mitteilen:

* [!DNL Target] Aktivität, die Ihre Besucher eingegeben haben
* Welche Erfahrung sie gesehen haben
* Welche Konversion erreicht wurde

Die [!DNL Adobe Experience Platform Web SDK] unterstützt zwei Arten der [!DNL Analytics] für [!UICONTROL Analytics for Target] (A4T)-Anwendungsfälle:

| Protokollierungsmethode | Beschreibung |
| --- | --- |
| Server-seitige [!DNL Analytics] | Alle [!DNL Analytics] über die Edge Network gesendeten Treffer werden Server-seitig um [!DNL Target] Details erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss. |
| Client-seitige [!DNL Analytics] | [!DNL Target] Daten werden Client-seitig zurückgegeben, sodass Sie Daten manuell erweitern und mit der Data Insertion[API an [!DNL Analytics] senden &#x200B;](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=de). |

Die Protokollierungsmethode wird davon bestimmt, ob Sie in Ihrem konfigurierten (Datenstrom[&#x200B; aktiviert [!DNL Adobe Analytics]](https://experienceleague.adobe.com/de/docs/experience-platform/datastreams/overview):

![Entscheidungsfluss der Protokollierungsmethode](/help/dev/implement/a4t/assets/analytics-logging.png)

## Nächste Schritte

Dieses Dokument bietet eine kurze Einführung in die verschiedenen Protokollierungsmethoden für A4T-Daten in der Web-SDK. Weitere Informationen zu den einzelnen Methoden finden Sie in der folgenden Dokumentation:

* [Server-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Client-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
