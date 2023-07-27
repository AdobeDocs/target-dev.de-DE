---
keywords: implementieren, implementieren, einrichten, einrichten, Datenanbieter
description: Daten abrufen [!DNL Target] Datenanbieter verwenden.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden von Datenanbietern?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 53%

---

# Datenanbieter

Datenanbieter sind eine Funktion, mit der Sie Daten von Drittanbietern einfach an weitergeben können. [!DNL Adobe Target].

>[!NOTE]
>
>Datenanbieter benötigen at.js 1.3 oder höher.

## Format

Die Einstellung `window.targetGlobalSettings.dataProviders` entspricht einer Reihe von Datenanbietern.

Weitere Informationen zur Struktur für die einzelnen Datenanbieter finden Sie unter [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Anwendungsbeispiele

Erfassen Sie Daten von Drittanbietern, wie z. B. einem Wetterdienst, einem DMP oder sogar Ihrem eigenen Webservice. Anschließend können Sie diese Daten zur Erstellung von Zielgruppen und zielgerichtetem Inhalt und zur Aufwertung des Benutzerprofils verwenden.

## Vorteile der Methode

Mit dieser Einstellung können Kunden Daten von Drittanbietern (wie Demandbase, BlueKai und benutzerdefinierten Diensten) erfassen und die Daten an übergeben. [!DNL Target] als Mbox-Parameter in der globalen Mbox-Anfrage.

Sie unterstützt die Sammlung von Daten von mehreren Anbietern über asynchrone und synchrone Anfragen.

Mit diesem Ansatz ist es ein Leichtes, Flicker- oder Standardinhalte zu verwalten und gleichzeitig unabhängige Timeouts für die einzelnen Anbieter festzulegen, um die Auswirkungen auf die Seitenleistung zu begrenzen

## Einschränkungen

Wenn Datenanbieter zu `window.targetGlobalSettings.dataProviders` asynchron sind, werden sie parallel ausgeführt. Die Besucher-API-Anfrage wird parallel mit den Funktionen ausgeführt, die zu `window.targetGlobalSettings.dataProviders` um eine minimale Wartezeit zu ermöglichen.

at.js versucht nicht, die Daten zwischenzuspeichern. Wenn der Datenanbieter die Daten nur einmal abruft, sollte er sicherstellen, dass die Daten zwischengespeichert werden, und die Cachedaten für den zweiten Aufruf verarbeiten, wenn die Anbieterfunktion aufgerufen wird.

## Codebeispiele

Unter [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers) finden Sie verschiedene Beispiele.

## Links zu relevanten Informationen

Dokumentation: [Datenanbieter](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Schulungsvideos:

* [Verwenden von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implementieren von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
