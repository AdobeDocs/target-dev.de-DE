---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Massen-Profil-Aktualisierungs-API
description: Holen Sie Daten in  [!DNL Target]  mithilfe der [!UICONTROL API zur Massenaktualisierung von Profilen].
title: Wie integriere ich Daten in  [!DNL Target]  mit der [!UICONTROL Bulk Profile Update API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 284
ht-degree: 5%

---

# API zur Massenaktualisierung von Profilen

Mit der [!DNL Adobe Target] [!UICONTROL API zur Massenaktualisierung von ]) können Sie Benutzerprofile für mehrere Besucher einer Website mithilfe einer Batch-Datei stapelweise aktualisieren.

Mit der [!UICONTROL Bulk Profile Update API] können Sie für viele Benutzer bequem detaillierte Besucherprofildaten in Form von Profilparametern senden, um sie aus einer beliebigen externen Quelle zu [!DNL Target]. Zu den externen Quellen können CRM (Customer Relationship Management)- oder POS (Point of Sale)-Systeme gehören, die normalerweise nicht auf einer Web-Seite verfügbar sind.

Vergleichen Sie die [!UICONTROL API für die Massenprofilaktualisierung] mit der [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Kundenattribute] im Vergleich zur [!UICONTROL API zur Massenaktualisierung von Profilen]

Diese Option ähnelt [[!UICONTROL Kundenattributen]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) mit einigen Unterschieden:

* [!UICONTROL Kundenattribute] Verwenden eines FTP-Uploads. Die [!UICONTROL Target Bulk Profile Update API] verwendet eine HTTP POST-API.
* [!UICONTROL Kundenattribut] Daten können für [!DNL Analytics] freigegeben werden. Die [!UICONTROL Massenprofil-Aktualisierung] kann nur in [!DNL Target] verwendet werden.
* [!UICONTROL Kundenattribute] Unterstützung beim Erstellen eines Profils für einen Benutzer, den [!DNL Target] noch nicht gesehen hat.
   * [!UICONTROL Bulk Profile Update API] v2: Sie müssen nicht alle Parameterwerte für jede `pcId` angeben. Profile werden für alle `pcId` oder `mbox3rdPartyId` erstellt, die nicht in [!DNL Target] gefunden werden.
   * [!UICONTROL Bulk Profile Update API] v1: Die [!UICONTROL Bulk Profile Update API] aktualisiert nur vorhandene [!DNL Target]. Wenn Sie v1 verwenden, werden Profile nicht für fehlende `pcIds` oder `mbox3rdPartyIds` erstellt.
* [!UICONTROL Kundenattribute] erfordern die Verwendung der [!UICONTROL Experience Cloud ID] (ECID) und die Verwendung einer Quell-ID, wie der CRM-ID oder der Treueprogramm-ID.
* Die [!UICONTROL Bulk Profile Update API] erfordert entweder die TNT-ID oder die `mbox3rdPartyId`.
* Folgende Zeichen können nicht gesendet werden `mbox3rdPartyID`: Plus-Zeichen (+) und Schrägstrich (/).

## Ressourcen

Weitere Informationen finden Sie unter:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)