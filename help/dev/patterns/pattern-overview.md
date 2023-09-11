---
title: Übersicht über Implementierungsmuster
description: Grundlegendes zur Verwendung von Implementierungsmustern
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Übersicht über Implementierungsmuster

[!DNL Adobe Target] Implementierungsmuster helfen Ihnen, die folgende Architektur für Ihre [!DNL Target] Implementierung.

Klicken Sie auf Bild , um den Vollbildmodus zu erweitern.

![Architekturdiagramm von Adobe Target](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Beachten Sie, dass die Zahlen im Bild nicht die Reihenfolge der Vorgänge angeben:

1. Client-seitige SDKs für [!DNL Adobe Target] und [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. ECID-Akquise-Aufruf
1. Bulk-Profil-Update-API und [!DNL Customer Attributes] (CA)-Dienst
1. Erfassung von Profildaten aus den Datenquellen des Kunden in [!DNL Target] Profilspeicher
1. Erfassen von Profil-/Verhaltensdaten und Auswählen, welches Erlebnis dem Endbenutzer angezeigt werden soll
1. Erlebnisse werden auf der Seite dargestellt
1. at.js rendert die Erlebnisse auf der Seite

Jedes Muster besteht aus verschiedenen Teilen. Jeder Teil entspricht einer kritischen Implementierungsanforderung für Ihre [!DNL Target] Implementierung.

Jeder Teil wird auf einer separaten Seite in diesem Handbuch erläutert. Beispiel: die [[!DNL Recommendations] Implementierungsmuster mit at.js](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) enthält die folgenden Seiten:

* SDK initialisieren
* Datenerfassung konfigurieren
* Render-Erlebnisse
* Benachrichtigen [!DNL Target]

