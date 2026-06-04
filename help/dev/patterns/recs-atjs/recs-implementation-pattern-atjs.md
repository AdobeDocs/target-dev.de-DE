---
title: Implementierungsmuster für Recommendations unter Verwendung von at.js
description: Erfahren Sie, wie Sie das Implementierungsmuster für Recommendations mit at.js verwenden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 155
ht-degree: 0%

---

# [!DNL Recommendations] von Implementierungsmustern mit at.js - Überblick

Dieses Implementierungsmuster hilft Ihnen, Ihre [!DNL Adobe Target Recommendations] Implementierung zu verstehen und zu erstellen, wenn Sie die [at.js-JavaScript-Bibliothek verwenden](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

Klicken Sie auf Bild , um es auf den Vollbildmodus zu erweitern.

![Architekturdiagramm für Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Beachten Sie, dass die Zahlen im Bild nicht die Reihenfolge der Vorgänge angeben:

1. Client-seitige SDKs für [!DNL Adobe Target] und [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API]
1. [!UICONTROL Experience Cloud-ID] (ECID)-Akquise-Aufruf
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
