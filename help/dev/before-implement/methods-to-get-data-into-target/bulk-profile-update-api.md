---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Massen-Profil-Update
description: Daten abrufen [!DNL Target] mit der Bulk-Profil-Update-API.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der Bulk-Profil-Update-API?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 3ae2391dea9994c0ddc1df39d74cccf6e067c1a4
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 57%

---

# API zur Bulk-Aktualisierung von Profilen

Senden Sie über API eine CSV-Datei an [!DNL Adobe Target] mit Besucherprofilaktualisierungen für viele Besucher. Jedes Besucherprofil kann mit mehreren In-Page-Profilattributen in einem Aufruf aktualisiert werden.

Diese Option ähnelt Kundenattributen mit einigen Unterschieden:

* Kundenattribute verwenden einen FTP-Upload während der [!UICONTROL Bulk-Profil-Update-API für Target] verwendet eine HTTP-POST-API.
* Daten von Kundenattributen können für [!DNL Analytics]. [!UICONTROL Bulk-Profil-Update ist nur in Target verwendbar.]
* Kundenattribute unterstützen das Erstellen eines Profils für einen Benutzer [!DNL Target] noch nicht gesehen. Die Bulk Profile Update API aktualisiert vorhandene [!DNL Target] nur Profile.
* Kundenattribute erfordern die Verwendung der Experience Cloud ID (ECID) und einer Quell-ID, z. B. der CRM-ID oder der Loyalitäts-ID.
* Die Bulk-Profil-Update-API benötigt entweder die TNT ID oder die `mbox3rdPartyId`.
* Folgende Zeichen können nicht gesendet werden `mbox3rdPartyID`: Plus-Zeichen (+) und Schrägstrich (/).

## Format

Die .csv -Datei muss sich auf jeden Besucher über dessen [!DNL Target] PCID oder `mbox3rdPartyId`. Die Experience Cloud ID (ECID) wird nicht unterstützt. Alle Profilattribute/-werte werden über die API angelegt und aktualisiert. Details zum Format finden Sie in der API-Dokumentation.

## Anwendungsbeispiele

Ihr CRM oder ein anderes internes System speichert wertvolle Daten über Ihre Besucher, die Sie konsistent in Target aktualisieren möchten, ohne die Profildaten in Ihrer Seitenimplementierung freizugeben.

## Vorteile der Methode

Keine Begrenzung der Anzahl der Profilattribute.

Profilattribute, die über die Website gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen

Die Batch-Datei muss kleiner als 50 MB sein. Außerdem sollte die Gesamtzeilenzahl 500.000 Zeilen pro Upload nicht überschreiten.

Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.

Die Anzahl der Zeilen, die Sie über einen Zeitraum von 24 Stunden in nachfolgenden Batches hochladen können, ist unbegrenzt. Allerdings kann der Importverlauf während der Geschäftszeiten gedrosselt werden, um sicherzustellen, dass andere Prozesse effizient ablaufen.

Aufeinanderfolgende [V2-Batchupdate-Aufrufe](https://developers.adobetarget.com/api/#updating-profiles) ohne dazwischenliegende Mbox-Aufrufe für dieselben thirdPartyIds überschreiben die Eigenschaften, die im ersten Batchupdate-Aufruf aktualisiert wurden.

## Codebeispiele

Siehe [Update von Profilen](https://developers.adobetarget.com/api/#updating-profiles).

### Links zu relevanten Informationen

[Update von Profilen](https://developers.adobetarget.com/api/#updating-profiles)
