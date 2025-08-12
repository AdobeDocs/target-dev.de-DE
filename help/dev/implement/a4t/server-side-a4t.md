---
title: Server-seitige Protokollierung für A4T-Daten in Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Server-seitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe der Experience Platform Web SDK aktivieren.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;Target;Web;SDK;Plattform;Protokollierung;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Server-seitige Protokollierung für A4T-Daten in [!DNL Experience Platform Web SDK]

Mit dem [!DNL Adobe Experience Platform Web SDK] können Sie [!UICONTROL Adobe Analytics for Target] (A4T)-Funktionen in [!UICONTROL Experience Platform Edge Network] implementieren. Wenn die Server-seitige Protokollierung aktiviert ist, werden alle [!DNL Analytics] über die Edge Network gesendeten Treffer mit [!DNL Target] Details auf der Server-Seite erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss.

Die Server-seitige Protokollierung für [!DNL Analytics] ist aktiviert, wenn [!DNL Analytics] in der Datenstromkonfiguration aktiviert ist:

![Analytics-Datenstromkonfiguration aktiviert](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

Das folgende Diagramm zeigt, wie Daten durch das System fließen, wenn die Server-seitige [!DNL Analytics] aktiviert ist:

![Server-seitiger Protokollierungsfluss](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Nächste Schritte

In diesem Handbuch wurde die Server-seitige Protokollierung für A4T-Daten in der Web-SDK behandelt. Weitere Informationen zum [ von A4T-Daten auf der Client](/help/dev/implement/a4t/client-side-logging.md)Seite finden Sie im Handbuch zur Client-seitigen Protokollierung .