---
title: Übersicht über Implementierungsmuster
description: Grundlegendes zur Verwendung von Implementierungsmustern
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e15513f5c52240536ccf41f16ba7f4dc6dbf9a04
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Übersicht über Implementierungsmuster

[!DNL Adobe Target] Implementierungsmuster helfen Ihnen, die folgende Architektur für Ihre [!DNL Target] Implementierung.

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

Jeder Teil wird in diesem Handbuch in einem separaten Thema erläutert. Beispiel: die [[!DNL Recommendations] Implementierungsmuster mit at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) enthält die folgenden Themen:

* SDK initialisieren
* Datenerfassung konfigurieren
* Render-Erlebnisse
* Benachrichtigen [!DNL Target]

