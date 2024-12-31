---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Massen-Profil-Aktualisierungs-API
description: Abrufen von Daten in [!DNL Target] mithilfe der -[!UICONTROL Bulk Profile Update API].
title: Wie integriere ich Daten in  [!DNL Target]  mit dem [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 7%

---

# API zur Massenaktualisierung von Profilen

Mit dem [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] können Sie Benutzerprofile für mehrere Besucher einer Website mithilfe einer Batch-Datei stapelweise aktualisieren.

Mit dem [!UICONTROL Bulk Profile Update API] können Sie bequem detaillierte Besucherprofildaten in Form von Profilparametern senden, damit viele Benutzer aus beliebigen externen Quellen [!DNL Target] können. Zu den externen Quellen können CRM (Customer Relationship Management)- oder POS (Point of Sale)-Systeme gehören, die normalerweise nicht auf einer Web-Seite verfügbar sind.

Vergleichen Sie die [!UICONTROL Bulk Profile Update API] mit der [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] versus [!UICONTROL Bulk Profile Update API]

Diese Option ähnelt [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) mit einigen Unterschieden:

* [!UICONTROL Customer attributes] einen FTP-Upload verwenden. Der [!UICONTROL Target Bulk Profile Update API] verwendet eine HTTP-POST-API.
* [!UICONTROL Customer attribute] Daten können für [!DNL Analytics] freigegeben werden. Die [!UICONTROL Bulk Profile Update] kann nur in [!DNL Target] verwendet werden.
* [!UICONTROL Customer attributes] Unterstützung für das Erstellen eines Profils für einen Benutzer, den [!DNL Target] noch nicht gesehen hat.
   * [!UICONTROL Bulk Profile Update API] v2: Sie müssen nicht alle Parameterwerte für jede `pcId` angeben. Profile werden für alle `pcId` oder `mbox3rdPartyId` erstellt, die nicht in [!DNL Target] gefunden werden.
   * [!UICONTROL Bulk Profile Update API] v1: Die [!UICONTROL Bulk Profile Update API] aktualisiert nur vorhandene [!DNL Target]. Wenn Sie v1 verwenden, werden Profile nicht für fehlende `pcIds` oder `mbox3rdPartyIds` erstellt.
* [!UICONTROL Customer attributes] erfordern die Verwendung der [!UICONTROL Experience Cloud ID] (ECID) und die Verwendung einer Quell-ID, wie z. B. der CRM-ID oder der Treueprogramm-ID.
* Für die [!UICONTROL Bulk Profile Update API] ist entweder die TNT-ID oder die `mbox3rdPartyId` erforderlich.
* Folgende Zeichen können nicht gesendet werden `mbox3rdPartyID`: Plus-Zeichen (+) und Schrägstrich (/).

## Ressourcen

Weitere Informationen finden Sie unter:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)