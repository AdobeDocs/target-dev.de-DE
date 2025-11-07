---
title: Protokollierung von Adobe Analytics for Target (A4T) in der Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Erfassung von Daten aus Adobe Analytics for Target (A4T) mit der Experience Platform Web SDK steuern.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;Protokollierung;Analytics;SDK;Web SDK;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# [!DNL Adobe Analytics for Target] (A4T)-Protokollierung in der [!DNL Experience Platform Web SDK]

Bei der Verwendung von [!DNL Adobe Target] für die Personalisierung können Sie auswählen, welches System Sie für die Leistungsmessung verwenden möchten. Jede [Target-Aktivität](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) ermöglicht die Auswahl zwischen [!DNL Target] Reporting und Adobe [!DNL Analytics] Reporting.

Wenn Sie [!DNL Analytics] Reporting verwenden, müssen [!DNL Target] den [!DNL Analytics] Folgendes mitteilen:

* [!DNL Target] Aktivität, die Ihre Besucher eingegeben haben
* Welche Erfahrung sie gesehen haben
* Welche Konversion erreicht wurde

Die [!DNL Adobe Experience Platform Web SDK] unterstützt zwei Arten der [!DNL Analytics] für [!UICONTROL Analytics for Target] (A4T)-Anwendungsfälle:

| Protokollierungsmethode | Beschreibung |
| --- | --- |
| Server-seitige [!DNL Analytics] | Alle [!DNL Analytics] über die Edge Network gesendeten Treffer werden Server-seitig um [!DNL Target] Details erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss. |
| Client-seitige [!DNL Analytics] | [!DNL Target] Daten werden Client-seitig zurückgegeben, sodass Sie Daten manuell erweitern und mit der Data Insertion[!DNL Analytics]API an [&#x200B; senden &#x200B;](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Die Protokollierungsmethode wird davon bestimmt, ob Sie in Ihrem konfigurierten (Datenstrom[!DNL Adobe Analytics] aktiviert [&#128279;](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview):

![Entscheidungsfluss der Protokollierungsmethode](/help/dev/implement/a4t/assets/analytics-logging.png)

## Nächste Schritte

Dieses Dokument bietet eine kurze Einführung in die verschiedenen Protokollierungsmethoden für A4T-Daten in der Web-SDK. Weitere Informationen zu den einzelnen Methoden finden Sie in der folgenden Dokumentation:

* [Server-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Client-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
