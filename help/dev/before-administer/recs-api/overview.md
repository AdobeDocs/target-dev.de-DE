---
title: Was ist die Adobe Recommendations-API?
description: Dieses Handbuch führt Entwicklerinnen und Entwicklern durch praktische Übungen zur Verwendung der Adobe Target Recommendations-APIs zum Konfigurieren und Verwalten von Recommendations-Katalogen und benutzerdefinierten Kriterien sowie zur Verwendung der Bereitstellungs-API zum Abrufen von Recommendations-Inhalten.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 3%

---

# Übersicht über die Adobe Recommendations-API

Zu den für Recommendations relevanten APIs gehören [Admin-APIs](../../before-administer/target-api-overview.md) mit denen Sie:

* Katalog mit empfohlenen Produkten oder Inhalten verwalten
* Verwalten von Recommendations-Algorithmen und -Aktivitäten

Wenn Sie die Target [Bereitstellungs-API](../../implement/delivery-api/overview.md) mit Recommendations verwenden, können Sie auch:

* Rufen Sie Empfehlungen in JSON-, HTML- oder XML-Objekten ab, damit sie in Web-, Mobile-, E-Mail-, Internet of Things (IOT)- und anderen Kanälen angezeigt werden können.

## Beschreibung

Dieses Handbuch zu den Recommendations-APIs führt Entwicklerinnen und Entwicklern praktische Übungen zum Verwenden der Recommendations-APIs zum Konfigurieren und Verwalten von Recommendations-Katalogen und benutzerdefinierten Kriterien sowie zum Verwenden der Bereitstellungs-API zum Abrufen von Recommendations-Inhalten. Am Ende werden Sie in der Lage sein,

* Konfigurieren und Verwalten von Entitäten mithilfe der Recommendations-API
* Konfigurieren und Verwalten benutzerdefinierter Kriterien mithilfe der Recommendations-API
* Erfahren Sie, wie Sie Recommendations mit der Bereitstellungs-API verwenden können, um Recommendations-Ergebnisse auf Geräten zu nutzen, die nicht zu HTML gehören

## Zielgruppe

Dieses Handbuch richtet sich an Entwicklerinnen und Entwickler, die noch nicht mit Target-APIs oder Recommendations-APIs vertraut sind.

## Voraussetzungen {#prerequisites}

Die Target-Admin-APIs erfordern eine Einrichtung der [Adobe-Authentifizierung](../configure-authentication.md). Stellen Sie sicher, dass Sie dies konfiguriert haben, bevor Sie die Recommendations-API verwenden.

## Ressourcen

Beachten Sie die folgenden Ressourcen, die erforderlich sind, um dieses Handbuch zu verstehen und es erfolgreich zu befolgen:

| Ressource | Details |
| --- | --- |
| Postman | Rufen Sie die [Postman](https://www.postman.com/downloads/)App für Ihr Betriebssystem ab. Postman Basic ist bei der Kontoerstellung kostenlos. Obwohl dies für die Verwendung von Adobe Target-APIs im Allgemeinen nicht erforderlich ist, erleichtert Postman API-Workflows und Adobe Target bietet mehrere Postman-Sammlungen, die die Ausführung seiner APIs und deren Funktionsweise erleichtern. Im weiteren Verlauf dieses Handbuchs werden Kenntnisse über Postman vorausgesetzt. Unterstützung erhalten Sie in der [Dokumentation zu Postman](https://learning.getpostman.com/). |
| Verweise | Im weiteren Verlauf dieses Handbuchs wird von der Vertrautheit mit den folgenden Ressourcen ausgegangen:<UL><li>[Adobe I/O GitHub](https://github.com/adobeio)</li><li>[Target Admin- und Profil-API-Dokumentation](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Dokumentation zur Recommendations-API](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
