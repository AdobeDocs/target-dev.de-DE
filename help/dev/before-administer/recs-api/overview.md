---
title: Was ist die Adobe Recommendations-API?
description: Dieses Handbuch führt Entwickler durch praktische Verfahren zur Konfiguration und Verwaltung von Recommendations-Katalogen und benutzerdefinierten Kriterien mithilfe der Adobe Target Recommendations-APIs sowie zur Verwendung der Bereitstellungs-API zum Abrufen von Empfehlungsinhalten.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Übersicht über die Adobe Recommendations API

Zu den für Recommendations relevanten APIs gehören [Admin-APIs](../../before-administer/target-api-overview.md), mit denen Sie:

* Verwalten Ihres Katalogs empfohlener Produkte oder Inhalte
* Recommendations-Algorithmen und -Aktivitäten verwalten

Mithilfe der Target-[Bereitstellungs-API](../../implement/delivery-api/overview.md) mit Recommendations können Sie auch:

* Rufen Sie Empfehlungen in JSON-, HTML- oder XML-Objekten ab, damit sie im Web, auf Mobilgeräten, in E-Mails, im Internet der Dinge (IOT) und anderen Kanälen angezeigt werden können.

## Beschreibung

In diesem Handbuch zu den Recommendations-APIs werden Entwickler durch praktische Verfahren geführt, mit denen sie die Recommendations-APIs zum Konfigurieren und Verwalten von Recommendations-Katalogen und benutzerdefinierten Kriterien sowie die Bereitstellungs-API zum Abrufen von Empfehlungsinhalten verwenden. Am Ende können Sie:

* Konfigurieren und Verwalten von Entitäten mithilfe der Recommendations-API
* Benutzerdefinierte Kriterien mithilfe der Recommendations-API konfigurieren und verwalten
* Erfahren Sie, wie Sie Recommendations mit der Bereitstellungs-API verwenden, um Empfehlungsergebnisse auf Nicht-HTML-Geräten zu verwenden.

## Zielgruppe

Dieses Handbuch richtet sich an Entwickler, die mit Target-APIs oder Recommendations-APIs neu sind.

## Voraussetzungen  {#prerequisites}

Für die Target-Admin-APIs ist die Einrichtung der Adobe-Authentifizierung ](../configure-authentication.md) erforderlich. [ Stellen Sie sicher, dass Sie diese Konfiguration vorgenommen haben, bevor Sie die Recommendations-API verwenden.

## Ressourcen

Beachten Sie die folgenden Ressourcen, die erforderlich sind, um dieses Handbuch zu verstehen und es erfolgreich zu befolgen:

| Ressource | Details |
| --- | --- |
| Postman | Rufen Sie die [Postman-App](https://www.postman.com/downloads/) für Ihr Betriebssystem ab. Postman Basic ist mit der Kontoerstellung kostenlos. Postman ist zwar nicht erforderlich, um Adobe Target-APIs im Allgemeinen zu verwenden, erleichtert aber API-Workflows. Adobe Target bietet mehrere Postman-Sammlungen, die die Ausführung seiner APIs erleichtern und erfahren, wie sie funktionieren. Der Rest dieses Handbuchs setzt Grundkenntnisse in Postman voraus. Hilfe finden Sie in der [Postman-Dokumentation](https://learning.getpostman.com/). |
| Verweise | Im Rest dieses Handbuchs wird davon ausgegangen, dass Sie mit den folgenden Ressourcen vertraut sind:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Dokumentation zur Target-Admin- und Profil-API](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API-Dokumentation](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
