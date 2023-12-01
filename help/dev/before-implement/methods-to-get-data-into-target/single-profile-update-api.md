---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Einzelprofil-Update
description: Daten abrufen [!DNL Target] Verwendung der API für die Aktualisierung einzelner Profile.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der [!UICONTROL Single Profile Update API]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# [!UICONTROL Single Profile Update API]

Die [!DNL Adobe Target] [!UICONTROL Single Profile Update API] ermöglicht den Versand einer Profilaktualisierung an einen einzelnen Benutzer. Die [!UICONTROL Single Profile Update API] ist fast identisch mit dem [!UICONTROL Bulk-Profil-Update-API], jedoch wird jeweils ein Besucherprofil aktualisiert, und zwar entsprechend dem API-Aufruf und nicht mit einer .cvs-Datei.

Die [!UICONTROL Single Profile Update API] und wird im Allgemeinen verwendet, wenn eine Aktualisierung für eine Transaktion vorgenommen werden muss, die in einem Kanal erfolgt, der nicht implementiert wurde [!DNL Target]. Sie möchten beispielsweise das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Zu den Aktionen gehören das Erreichen eines Callcenters, die Finanzierung eines Darlehens, die Verwendung einer Treuekarte im Geschäft, der Zugriff auf einen Kiosk usw.

## Ressourcen:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
