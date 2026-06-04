---
title: Server-seitige Protokollierung für A4T-Daten in Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Server-seitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe der Experience Platform Web SDK aktivieren.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;Target;Web;SDK;Plattform;Protokollierung;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 161
ht-degree: 0%

---

# Server-seitige Protokollierung für A4T-Daten in [!DNL Experience Platform Web SDK]

Mit dem [!DNL Adobe Experience Platform Web SDK] können Sie die Funktion [!UICONTROL Adobe Analytics for Target] (A4T) in [!UICONTROL Experience Platform Edge Network&rbrace; &#x200B;]. Wenn die Server-seitige Protokollierung aktiviert ist, werden alle [!DNL Analytics] über die Edge Network gesendeten Treffer mit [!DNL Target] Details auf der Server-Seite erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss.

Die Server-seitige Protokollierung für [!DNL Analytics] ist aktiviert, wenn [!DNL Analytics] in der Datenstromkonfiguration aktiviert ist:

![Analytics-Datenstromkonfiguration aktiviert](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

Das folgende Diagramm zeigt, wie Daten durch das System fließen, wenn die Server-seitige [!DNL Analytics] aktiviert ist:

![Server-seitiger Protokollierungsfluss](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Nächste Schritte

In diesem Handbuch wurde die Server-seitige Protokollierung für A4T-Daten in der Web-SDK behandelt. Weitere Informationen zum [&#x200B; von A4T-Daten auf der Client](/help/dev/implement/a4t/client-side-logging.md)Seite finden Sie im Handbuch zur Client-seitigen Protokollierung .
