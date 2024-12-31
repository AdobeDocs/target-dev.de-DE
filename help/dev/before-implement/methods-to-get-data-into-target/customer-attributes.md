---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Kundenattribute
description: Abrufen von Daten in [!DNL Target] mithilfe von Kundenattributen.
title: Wie integriere ich Daten in  [!DNL Target]  mit Kundenattributen?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 14%

---

# Kundenattribute

Mit Kundenattributen können Sie Besucherprofildaten per FTP in die [!DNL Adobe Experience Cloud] hochladen. Verwenden Sie die Daten nach dem Hochladen in [!DNL Adobe Analytics] und [!DNL Adobe Target].

Target Standard-Kunden können fünf Attribute anwenden, [!DNL Target Premium] Kunden können 200 Attribute anwenden.

## Format

Eine CSV-Datei mit [!DNL Experience Cloud]-IDs (ECIDs) und Attributnamen/Attributwertpaaren wird per FTP oder manuell in die Experience Cloud-Benutzeroberfläche hochgeladen.

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
