---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Aktualisierung einzelner Profile
description: Daten in abrufen [!DNL Target] mithilfe der API zur Aktualisierung von einzelnen Profilen.
title: Wie integriere ich Daten in  [!DNL Target]  mit dem [!UICONTROL Single Profile Update API]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
TQID: https://experienceleague.adobe.com/tkh7YEJ9Vr5eMynNYYxYKZZDOXZTVJNxwUSCxiwPfzI
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
source-wordcount: 132
ht-degree: 3%

---

# [!UICONTROL Single Profile Update API]

Mit dem [!DNL Adobe Target] [!UICONTROL Single Profile Update API] können Sie eine Profilaktualisierung für einen einzelnen Benutzer senden. Der [!UICONTROL Single Profile Update API] ist fast identisch mit dem [!UICONTROL Bulk Profile Update API], aber es wird jeweils ein Besucherprofil aktualisiert, und zwar inline mit dem API-Aufruf anstelle mit einer .cvs-Datei.

Die [!UICONTROL Single Profile Update API] und werden im Allgemeinen verwendet, wenn eine Aktualisierung in Bezug auf eine Transaktion erfolgen muss, die in einem Kanal stattfindet, der [!DNL Target] nicht implementiert wurde. Sie möchten beispielsweise das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Aktionen können das Erreichen eines Callcenters, ein Kredit wird finanziert, eine Kundenkarte im Geschäft verwenden, auf einen Kiosk zugreifen und so weiter.

Vergleichen Sie die [!UICONTROL Single Profile Update API] mit der [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## Ressourcen

Weitere Informationen finden Sie unter:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
