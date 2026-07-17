---
title: Übersicht über die Adobe Target-Bereitstellungs-API
description: Übersicht über die Adobe Target-Bereitstellungs-API
keywords: Bereitstellungs-API
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gPXGax6ccvZZPklT3jnZbqyOj3mCClEfSpdufAFPtSs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: b6b447ccb88925a8efb6ff6a80ae475c8780dbc8
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 0%

---

# Übersicht über die Bereitstellungs-API

Die [!DNL Adobe Target Delivery API] basiert auf REST. In dieser Dokumentation werden die Ressourcen beschrieben, aus denen die [!DNL Adobe Target] [!DNL Delivery API] besteht. HTTP-Methoden werden verwendet, um Vorgänge für diese Ressourcen auszuführen.

>[!IMPORTANT]
>
>Die hier dokumentierte [!DNL Delivery API] ist für [!DNL at.js] und direkte Server-seitige Implementierungen vorgesehen. Wenn Sie [!DNL Target] mithilfe der [!DNL Adobe Experience Platform Web SDK] implementieren, verwenden Sie die Interact-API, auf die über den `sendEvent`-Befehl über die [!UICONTROL Experience Platform-Edge Network] zugegriffen wird, anstatt die [!DNL Delivery API] direkt aufzurufen. Weitere Informationen finden Sie unter &lbrace;0[&#128279;](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) Adobe Experience Platform Web SDK[&#x200B; und Vergleichen der at.js-Bibliothek mit der Experience Platform Web &#x200B;](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)SDK).

Mit der Bereitstellungs-API von {}Adobe Target haben Sie folgende Möglichkeiten:

* Bereitstellen von Erlebnissen im Web, einschließlich SPAs und mobilen Kanälen sowie Nicht-Browser-basierten IoT-Geräten wie einem verbundenen TV, Kiosk oder digitalen Bildschirmen im Geschäft.
* Bereitstellen von Erlebnissen von jeder Server-seitigen Plattform oder Anwendung, die HTTP/s-Aufrufe ausführen kann.
* Bereitstellen konsistenter und personalisierter Erlebnisse für Benutzer, unabhängig davon, über welchen Kanal oder welche Geräte der Benutzer mit Ihrem Unternehmen interagiert hat.
* Speichern Sie Erlebnisse für einen Benutzer innerhalb einer Sitzung auf Ihrem Server zwischen, damit mehrere API-Aufrufe vermieden werden können und so eine bessere Leistung erzielt wird.
* Nahtlose Integration mit [!DNL Adobe Experience Cloud] Produkten wie [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] und dem [!DNL Experience Cloud ID Service] von der Serverseite aus.

>[!NOTE]
>
>Sie können weiterhin auf die [alte /v1/mbox- und /v2/batchmbox-API-Dokumentation](https://developers.adobetarget.com/api/legacy-api/index.html) zugreifen. Funktionen werden jedoch in der Bereitstellungs-API entwickelt (wie hier dokumentiert) und nicht in die Legacy-APIs rückportiert.
