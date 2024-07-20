---
title: Recommendations-Implementierungsmuster mit at.js
description: Grundlegendes zur Verwendung des Implementierungsmusters für Recommendations mit at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!DNL Recommendations] Implementierungsmuster mit at.js - Übersicht

Dieses Implementierungsmuster hilft Ihnen beim Verständnis und Erstellen Ihrer [!DNL Adobe Target Recommendations] -Implementierung bei der Verwendung der [at.js JavaScript-Bibliothek](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Klicken Sie auf Bild , um den Vollbildmodus zu erweitern.

![Adobe Target-Architekturdiagramm](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Beachten Sie, dass die Zahlen im Bild nicht die Reihenfolge der Vorgänge angeben:

1. Client-seitige SDKs für [!DNL Adobe Target] und [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] Aufruf
1. Akquise-Aufruf [!UICONTROL Experience Cloud ID] (ECID)
1. Bulk-Profil-Update-API und -Dienst [!DNL Customer Attributes] (CA)
1. Profildatenerfassung aus den Datenquellen des Kunden in den [!DNL Target] Profilspeicher
1. Erfassen von Profil- und Verhaltensdaten und Auswählen, welches Erlebnis dem Besucher angezeigt werden soll
1. Erlebnisse werden auf der Seite dargestellt
1. at.js rendert die Erlebnisse auf der Seite

Jedes Muster besteht aus verschiedenen Teilen, wobei jeder Teil einer kritischen Implementierungsanforderung für Ihre [!DNL Target] -Implementierung entspricht.

Jeder Teil wird in einem separaten Artikel in diesem Handbuch erläutert:

* [SDKS initialisieren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Datenerfassung konfigurieren](/help/dev/patterns/recs-atjs/data-collection.md)
* [Erlebnisse rendern](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Target benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md)
