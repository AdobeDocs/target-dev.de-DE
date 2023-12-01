---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Massen-Profil-Update-API
description: Daten abrufen [!DNL Target] mithilfe der [!UICONTROL Bulk-Profil-Update-API].
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der [!UICONTROL Bulk-Profil-Update-API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 4%

---

# Bulk-Profil-Update-API

Die [!DNL Adobe Target] [!UICONTROL Bulk-Profil-Update-API] ermöglicht Ihnen, mithilfe einer Batch-Datei Benutzerprofile für mehrere Besucher einer Website stapelweise zu aktualisieren.

Verwenden der [!UICONTROL Bulk-Profil-Update-API]können Sie detaillierte Besucherprofildaten in Form von Profilparametern für viele Benutzer an senden. [!DNL Target] aus einer beliebigen externen Quelle. Externe Quellen können beispielsweise CRM-Systeme (Customer Relationship Management) oder POS-Systeme (Point of Sale) sein, die normalerweise nicht auf einer Webseite verfügbar sind.

## [!UICONTROL Kundenattribute] versus [!UICONTROL Bulk-Profil-Update-API]

Diese Option ähnelt der [!UICONTROL Kundenattribute] mit einigen Unterschieden:

* [!UICONTROL Kundenattribute] FTP-Upload verwenden. Die [!UICONTROL Bulk-Profil-Update-API für Target] verwendet eine HTTP-POST-API.
* [!UICONTROL Kundenattribut] Daten können für [!DNL Analytics]. Die [!UICONTROL Massenprofilaktualisierung] ist nur in [!DNL Target].
* [!UICONTROL Kundenattribute] Unterstützung beim Erstellen eines Profils für einen Benutzer [!DNL Target] noch nicht gesehen.
   * [!UICONTROL Bulk-Profil-Update-API] v2: Sie müssen nicht alle Parameterwerte für jede `pcId`. Profile werden für alle `pcId` oder `mbox3rdPartyId` das nicht in [!DNL Target].
   * [!UICONTROL Bulk-Profil-Update-API] v1: Die [!UICONTROL Bulk-Profil-Update-API] vorhandene aktualisieren [!DNL Target] nur Profile. Wenn Sie v1 verwenden, werden Profile nicht für fehlende erstellt `pcIds` oder `mbox3rdPartyIds`.
* [!UICONTROL Kundenattribute] die Verwendung der [!UICONTROL Experience Cloud-ID] (ECID) und die Verwendung einer Quell-ID, z. B. der CRM-ID oder der Loyalitäts-ID.
* Die [!UICONTROL Bulk-Profil-Update-API] erfordert entweder die TNT-ID oder die `mbox3rdPartyId`.
* Folgende Zeichen können nicht gesendet werden `mbox3rdPartyID`: Plus-Zeichen (+) und Schrägstrich (/).

## Ressourcen

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)