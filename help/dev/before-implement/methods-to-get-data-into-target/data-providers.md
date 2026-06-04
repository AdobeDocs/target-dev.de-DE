---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Datenanbieter
description: Daten in abrufen [!DNL Target] mithilfe von Datenanbietern.
title: Wie integriere ich Daten in  [!DNL Target]  mit Datenanbietern?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
TQID: https://experienceleague.adobe.com/e8uMaGcACjHiaIT4WSlbKry82mhLHUDTSKmCuuhoWgw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 50%

---

# Datenanbieter

Datenanbieter sind eine Funktion, mit der Sie Daten einfach von Drittanbietern an [!DNL Adobe Target] weitergeben können.

>[!NOTE]
>
>Datenanbieter benötigen at.js 1.3 oder höher.

## Format

Die Einstellung `window.targetGlobalSettings.dataProviders` entspricht einer Reihe von Datenanbietern.

Weitere Informationen zur Struktur für die einzelnen Datenanbieter finden Sie unter [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Anwendungsbeispiele

Erfassen Sie Daten von Drittanbietern, wie z. B. einem Wetterdienst, einem DMP oder sogar Ihrem eigenen Webservice. Anschließend können Sie diese Daten zur Erstellung von Zielgruppen und zielgerichtetem Inhalt und zur Aufwertung des Benutzerprofils verwenden.

## Vorteile der -Methode

Mit dieser Einstellung können Kundinnen und Kunden Daten von Drittanbieterdatenanbietern wie Demandbase, BlueKai und benutzerdefinierten Services erfassen und die Daten als Mbox-Parameter in der globalen Mbox-Anfrage an [!DNL Target] übergeben.

Sie unterstützt die Sammlung von Daten von mehreren Anbietern über asynchrone und synchrone Anfragen.

Mit diesem Ansatz ist es ein Leichtes, Flicker- oder Standardinhalte zu verwalten und gleichzeitig unabhängige Timeouts für die einzelnen Anbieter festzulegen, um die Auswirkungen auf die Seitenleistung zu begrenzen

## Einschränkungen

Wenn die zu `window.targetGlobalSettings.dataProviders` hinzugefügten Datenanbieter asynchron sind, werden sie parallel ausgeführt. Die Besucher-API-Anfrage wird parallel mit Funktionen ausgeführt, die zu `window.targetGlobalSettings.dataProviders` hinzugefügt werden, um eine minimale Wartezeit zu ermöglichen.

at.js versucht nicht, die Daten zwischenzuspeichern. Wenn der Datenanbieter die Daten nur einmal abruft, sollte er sicherstellen, dass die Daten zwischengespeichert werden, und die Cachedaten für den zweiten Aufruf verarbeiten, wenn die Anbieterfunktion aufgerufen wird.

## Code-Beispiele

Unter [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers) finden Sie verschiedene Beispiele.

## Links zu relevanten Informationen

Dokumentation: [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Schulungsvideos:

* [Verwenden von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implementieren von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
