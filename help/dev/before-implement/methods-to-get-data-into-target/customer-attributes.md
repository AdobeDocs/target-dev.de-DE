---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Kundenattribute
description: Abrufen von Daten in [!DNL Target] mithilfe von Kundenattributen.
title: Wie integriere ich Daten in  [!DNL Target]  mit Kundenattributen?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
TQID: https://experienceleague.adobe.com/bzK915y7fvjfZjTkSK2QWHDzmIN9SdAQiEguiUlc-r8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 216
ht-degree: 13%

---

# Kundenattribute

Mit Kundenattributen können Sie Besucherprofildaten per FTP in die [!DNL Adobe Experience Cloud] hochladen. Verwenden Sie die Daten nach dem Hochladen in [!DNL Adobe Analytics] und [!DNL Adobe Target].

Target Standard-Kunden können fünf Attribute anwenden, [!DNL Target Premium] Kunden können 200 Attribute anwenden.

## Format

Eine CSV-Datei mit [!DNL Experience Cloud]-IDs (ECIDs) und Attributnamen/Attributwert-Paaren wird per FTP oder manuell in die Experience Cloud-Benutzeroberfläche hochgeladen.

## Anwendungsbeispiele

Ihr CRM-System oder ein anderes internes System speichert wertvolle Informationen, die Sie mit [!DNL Adobe Experience Cloud] teilen möchten, einschließlich [!DNL Target] und [!DNL Analytics].

## Vorteile der -Methode

Beim Hochladen von Kundendaten wird ein Profileintrag für diesen Besucher in Target erstellt, auch wenn [!DNL Target] den Besucher noch nicht gesehen hat.

Dieselben Daten sind automatisch in [!DNL Target] und [!DNL Analytics] verfügbar.

FTP kann eine einfachere Implementierungsmethode als API sein.

## Einschränkungen

Target Standard-Kunden können fünf Attribute anwenden, [!DNL Target Premium] Kunden können 200 Attribute anwenden

Kann nur Werte über Kundenattribute aktualisieren, nicht auf der Seite.

Erfordert die Implementierung von Experience Cloud ID (ECID).

## Code-Beispiele

Details finden Sie unter [Erstellen einer Kundenattributquelle und Hochladen der Datendatei](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### Links zu relevanten Informationen

[Erstellen einer Kundenattributquelle und Hochladen der Datendatei](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
