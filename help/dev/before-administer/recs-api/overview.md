---
title: Was ist die Adobe Recommendations-API?
description: Dieses Handbuch führt Entwicklerinnen und Entwicklern durch praktische Übungen zur Verwendung der Adobe Target Recommendations-APIs zum Konfigurieren und Verwalten von Recommendations-Katalogen und benutzerdefinierten Kriterien sowie zur Verwendung der Bereitstellungs-API zum Abrufen von Recommendations-Inhalten.
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

# Übersicht über die Adobe Recommendations-API

Zu den für Recommendations relevanten APIs gehören [Admin-](../../before-administer/target-api-overview.md)), mit denen Sie:

* Katalog mit empfohlenen Produkten oder Inhalten verwalten
* Verwalten von Recommendations-Algorithmen und -Aktivitäten

Mit der Target [Bereitstellungs-API](../../implement/delivery-api/overview.md) mit Recommendations können Sie auch:

* Rufen Sie Empfehlungen in JSON-, HTML- oder XML-Objekten ab, damit sie in Web-, Mobile-, E-Mail-, Internet der Dinge (IOT) und anderen Kanälen angezeigt werden können.

## Beschreibung

Dieses Handbuch zu den Recommendations-APIs führt Entwicklerinnen und Entwickler durch die praktische Verwendung der Recommendations-APIs zum Konfigurieren und Verwalten von Recommendations-Katalogen und benutzerdefinierten Kriterien sowie die Verwendung der Bereitstellungs-API zum Abrufen von Recommendations-Inhalten. Am Ende werden Sie in der Lage sein,

* Konfigurieren und Verwalten von Entitäten mit der Recommendations-API
* Konfigurieren und Verwalten benutzerdefinierter Kriterien mithilfe der Recommendations-API
* Erfahren Sie, wie Sie Recommendations mit der Bereitstellungs-API verwenden können, um Recommendations-Ergebnisse auf Nicht-HTML-Geräten zu verwenden

## Zielgruppe

Dieses Handbuch richtet sich an Entwicklerinnen und Entwickler, die noch nicht mit Target-APIs oder Recommendations-APIs vertraut sind.

## Voraussetzungen  {#prerequisites}

Die Target-Admin-APIs erfordern eine Einrichtung der [Adobe-Authentifizierung](../configure-authentication.md). Stellen Sie sicher, dass Sie dies konfiguriert haben, bevor Sie die Recommendations-API verwenden.

## Ressourcen

Beachten Sie die folgenden Ressourcen, die erforderlich sind, um dieses Handbuch zu verstehen und es erfolgreich zu befolgen:

| Ressource | Details |
| --- | --- |
| Postman | Rufen Sie die [Postman](https://www.postman.com/downloads/)App für Ihr Betriebssystem ab. Postman Basic ist bei der Kontoerstellung kostenlos. Obwohl dies für die Verwendung von Adobe Target-APIs im Allgemeinen nicht erforderlich ist, erleichtert Postman API-Workflows und Adobe Target bietet mehrere Postman-Sammlungen, die die Ausführung seiner APIs und deren Funktionsweise erleichtern. Im weiteren Verlauf dieses Handbuchs werden Kenntnisse über Postman vorausgesetzt. Unterstützung erhalten Sie in der [Dokumentation zu Postman](https://learning.getpostman.com/). |
| Verweise | Im weiteren Verlauf dieses Handbuchs wird von der Vertrautheit mit den folgenden Ressourcen ausgegangen:<UL><li>[Adobe I/O GitHub](https://github.com/adobeio)</li><li>[Target Admin- und Profil-API-Dokumentation](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Dokumentation zur Recommendations-API](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
