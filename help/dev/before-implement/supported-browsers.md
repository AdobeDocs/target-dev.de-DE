---
keywords: Browser, Voraussetzungen, Anforderungen, Internet Explorer, Chrome, Firefox, Safari, Android, Oberfläche, Browser0
description: Erfahren Sie, welche Internet-Browser [!DNL Adobe Target] für die Benutzeroberfläche und die Inhaltsbereitstellung unterstützen.
title: Welche Browser werden von [!DNL Target] unterstützt?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 26%

---

# Unterstützte Browser

Die Bereitstellung der [!DNL Adobe Target]-Anwendung und von Inhalten wurde für eine breite Auswahl von Browsern und Geräten geprüft.

Weitere wichtige Informationen zu TLS finden Sie unter [TLS (Transport Layer Security)-Verschlüsselungsänderungen](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standard/Premium-Benutzeroberfläche

Die Oberfläche von [!DNL Target] unterstützt die folgenden Browser und Geräte:

| Gerätetyp | Browser-Version |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome (neueste Version, letzte minus 1)</li><li>Mozilla Firefox (neueste Version, neueste Version minus 1)</li></ul> |
| Mac | <ul><li>Firefox (neueste Version, neueste Version minus 1)</li><li>Chrome (neueste Version, neueste Version minus 1)</li></ul> |

## Inhaltsbereitstellung

Die Inhaltsbereitstellung wurde für folgende Browser und Geräte getestet:

| Gerätetyp | Browser-Version |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 und 10. Im Emulationsmodus getestet. **Hinweis**: Die Inhaltsbereitstellung in IE 9 wird in at.js 1.3.0 (und höher) nicht mehr unterstützt. Die Inhaltsbereitstellung in IE 10, 11 und allen älteren Versionen wird in at.js 2.5.0 (und höher) nicht mehr unterstützt.</li><li>Internet Explorer 11. **Hinweis**: Die Inhaltsbereitstellung in IE 10, 11 und allen älteren Versionen wird in at.js 2.5.0 (und höher) nicht mehr unterstützt.</li><li>Microsoft Edge</li><li>Chrome (neueste Version, neueste Version minus 1)</li><li>Firefox (neueste Version, neueste Version minus 1)</li></ul> |
| Mac | <ul><li>Apple Safari (neueste Version). **Hinweis**: Weitere Informationen dazu, wie Safari mit Erst- und Drittanbieter-Cookies umgeht, finden Sie unter [Target-Cookie](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (neueste Version, neueste Version minus 1)</li><li>Chrome (neueste Version, neueste Version minus 1)</li></ul> |
| Mobiltelefon/Tablet | <ul><li>Apple iOS (neueste Version)</li><li>Android-Geräte und -Tablets (Android 4 und neuer)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Beachten Sie Folgendes:

* Bei at.js-Implementierungen zeigt [!DNL Target] Standardinhalte in früheren Versionen von Internet Explorer und möglicherweise in älteren Versionen der oben aufgeführten Browser an.
* Internet Explorer behandelt alle unbekannten Elemente (z. B. benutzerdefinierte Elemente) als denselben Elementtyp. Daher funktioniert der Versand nicht mit benutzerdefinierten Elementen.
* [!DNL Target] zeigt Standardinhalte in Browsern an, die oben nicht aufgeführt sind, und in Browsern, die den [Quirks-Modus](https://en.wikipedia.org/wiki/Quirks_mode) verwenden. Für at.js ist ein Dokumenttyp erforderlich, der im Standardmodus dargestellt wird, beispielsweise `<!DOCTYPE html>`.
* [!DNL Adobe] Die Bereitstellungsinfrastruktur wird gesichert, sodass TLS 1.0-Geräte und -Browser nach dem 12. September 2018 NICHT mehr unterstützt werden. Siehe [Änderungen hinsichtlich der Verschlüsselung mit TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md), um die Gesamtauswirkungen dieser Änderung zu verstehen.
