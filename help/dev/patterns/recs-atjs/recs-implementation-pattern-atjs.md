---
title: Implementierungsmuster für Recommendations unter Verwendung von at.js
description: Erfahren Sie, wie Sie das Implementierungsmuster für Recommendations mit at.js verwenden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# [!DNL Recommendations] von Implementierungsmustern mit at.js - Überblick

Dieses Implementierungsmuster hilft Ihnen, Ihre [!DNL Adobe Target Recommendations] Implementierung zu verstehen und zu erstellen, wenn Sie die [at.js-JavaScript-Bibliothek verwenden](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

Klicken Sie auf Bild , um es auf den Vollbildmodus zu erweitern.

![Architekturdiagramm für Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Beachten Sie, dass die Zahlen im Bild nicht die Reihenfolge der Vorgänge angeben:

1. Client-seitige SDKs für [!DNL Adobe Target] und [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API]
1. [!UICONTROL Experience Cloud ID] (ECID)-Akquise-Aufruf
1. API- und [!DNL Customer Attributes]-Service (CA) für die Massenaktualisierung von Profilen
1. Profildatenaufnahme aus den Datenquellen des Kunden in [!DNL Target] Profilspeicher
1. Erfassen von Profil- und Verhaltensdaten und Festlegen des Erlebnisses, das dem Besucher angezeigt werden soll
1. Erlebnisse auf der Seite rendern
1. at.js rendert die Erlebnisse auf der Seite

Jedes Muster besteht aus verschiedenen Teilen, wobei jeder Teil einer kritischen Implementierungsanforderung für Ihre [!DNL Target] Implementierung entspricht.

Jeder Teil wird in einem separaten Artikel in diesem Handbuch erläutert:

* [SDKS initialisieren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Konfigurieren der Datenerfassung](/help/dev/patterns/recs-atjs/data-collection.md)
* [Rendern von Erlebnissen](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Zielgruppe benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md)
