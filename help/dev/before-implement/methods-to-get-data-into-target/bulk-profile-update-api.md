---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Massen-Profil-Update-API
description: Daten abrufen [!DNL Target] mithilfe der [!UICONTROL Bulk-Profil-Update-API].
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der [!UICONTROL Bulk-Profil-Update-API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 734bda64915a08f2edba37cbbb66b2de581c2237
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 30%

---

# Bulk-Profil-Update-API

Senden Sie über API eine CSV-Datei an [!DNL Adobe Target] mit Besucherprofilaktualisierungen für viele Besucher. Jedes Besucherprofil kann mit mehreren In-Page-Profilattributen in einem Aufruf aktualisiert werden.

Diese Option ähnelt der [!UICONTROL Kundenattribute] mit einigen Unterschieden:

* [!UICONTROL Kundenattribute] FTP-Upload verwenden. Die [!UICONTROL Bulk-Profil-Update-API für Target] verwendet eine HTTP-POST-API.
* [!UICONTROL Kundenattribut] Daten können für [!DNL Analytics]. [!UICONTROL Massenprofilaktualisierung] ist nur in [!DNL Target].
* [!UICONTROL Kundenattribute] Unterstützung beim Erstellen eines Profils für einen Benutzer [!DNL Target] noch nicht gesehen.
   * [!UICONTROL Bulk-Profil-Update-API] v2: Sie müssen nicht alle Parameterwerte für jede `pcId`. Profile werden für alle `pcId` oder `mbox3rdPartyId` das nicht in [!DNL Target].
   * [!UICONTROL Bulk-Profil-Update-API] v1: Die [!UICONTROL Bulk-Profil-Update-API] vorhandene aktualisieren [!DNL Target] nur Profile. Wenn Sie v1 verwenden, werden Profile nicht für fehlende erstellt `pcIds` oder `mbox3rdPartyIds`.
* [!UICONTROL Kundenattribute] die Verwendung der [!UICONTROL Experience Cloud-ID] (ECID) und die Verwendung einer Quell-ID, z. B. der CRM-ID oder der Loyalitäts-ID.
* Die [!UICONTROL Bulk-Profil-Update-API] erfordert entweder die TNT-ID oder die `mbox3rdPartyId`.
* Folgende Zeichen können nicht gesendet werden `mbox3rdPartyID`: Plus-Zeichen (+) und Schrägstrich (/).

## Format

Die .csv -Datei muss sich auf jeden Besucher über dessen [!DNL Target] PCID oder `mbox3rdPartyId`. Die [!UICONTROL Experience Cloud-ID] (ECID) wird nicht unterstützt. Alle Profilattribute/-werte werden über die API angelegt und aktualisiert. Details zum Format finden Sie in der API-Dokumentation.

## Anwendungsbeispiele

Ihr CRM-System oder ein anderes internes System speichert wertvolle Daten über Ihre Besucher, die Sie konsistent in [!DNL Target], ohne die Profildaten in Ihrer Seitenimplementierung verfügbar zu machen.

## Vorteile der Methode

* Keine Begrenzung der Anzahl der Profilattribute.
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen

* Die Batch-Datei muss kleiner als 50 MB sein. Außerdem sollte die Gesamtzeilenzahl 500.000 Zeilen pro Upload nicht überschreiten.
* Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.
* Die Anzahl der Zeilen, die Sie über einen Zeitraum von 24 Stunden in nachfolgenden Batches hochladen können, ist nicht beschränkt. Allerdings kann der Importverlauf während der Geschäftszeiten gedrosselt werden, um sicherzustellen, dass andere Prozesse effizient ablaufen.
* Aufeinanderfolgende [V2-Batchupdate-Aufrufe](https://developers.adobetarget.com/api/#updating-profiles)`thirdPartyIds` ohne dazwischenliegende Mbox-Aufrufe für dieselben überschreiben die Eigenschaften, die im ersten Batchupdate-Aufruf aktualisiert wurden.

## Codebeispiele

Siehe [Update von Profilen](https://developers.adobetarget.com/api/#updating-profiles).

### Links zu relevanten Informationen

[Update von Profilen](https://developers.adobetarget.com/api/#updating-profiles)
