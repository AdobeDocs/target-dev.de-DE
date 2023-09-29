---
title: Recommendations-Implementierungsmuster mit at.js
description: Grundlegendes zur Verwendung des Implementierungsmusters für Recommendations mit at.js
feature: APIs/SDKs
level: Experienced
role: Developer
source-git-commit: 723bb2f33a011995757009193ee9c48757ae1213
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!DNL Recommendations] Implementierungsmuster mit at.js - Übersicht

Dieses Implementierungsmuster hilft Ihnen beim Verständnis und Erstellen Ihrer [!DNL Adobe Target Recommendations] Implementierung bei Verwendung der [JavaScript-Bibliothek &quot;at.js&quot;](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

Klicken Sie auf Bild , um den Vollbildmodus zu erweitern.

![Architekturdiagramm von Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Beachten Sie, dass die Zahlen im Bild nicht die Reihenfolge der Vorgänge angeben:

1. Client-seitige SDKs für [!DNL Adobe Target] und [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. [!UICONTROL Experience Cloud-ID] (ECID)-Akquise-Aufruf
1. Bulk-Profil-Update-API und [!DNL Customer Attributes] (CA)-Dienst
1. Erfassung von Profildaten aus den Datenquellen des Kunden in [!DNL Target] Profilspeicher
1. Erfassen von Profil- und Verhaltensdaten und Auswählen, welches Erlebnis dem Besucher angezeigt werden soll
1. Erlebnisse werden auf der Seite dargestellt
1. at.js rendert die Erlebnisse auf der Seite

Jedes Muster besteht aus verschiedenen Teilen, wobei jedes Teil einer kritischen Implementierungsanforderung für Ihre [!DNL Target] Implementierung.

Jeder Teil wird in einem separaten Artikel in diesem Handbuch erläutert:

* [SDKS initialisieren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Datenerfassung konfigurieren](/help/dev/patterns/recs-atjs/data-collection.md)
* [Erlebnisse rendern](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Target benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md)

