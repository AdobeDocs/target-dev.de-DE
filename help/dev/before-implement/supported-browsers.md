---
keywords: Browser, Voraussetzungen, Anforderungen, Internet Explorer, Chrome, Firefox, Safari, Android, Oberfläche, Browser0
description: Erfahren Sie, welche Internet [!DNL Adobe Target] Browser die Benutzeroberfläche und die Bereitstellung von Inhalten unterstützen.
title: Welche Browser werden  [!DNL Target]  unterstützt?
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: 1b6dcb24d677b758ed1daf85dc0a7e9e5b42680d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 20%

---

# Unterstützte Browser

Die Bereitstellung der [!DNL Adobe Target]-Anwendung und von Inhalten wurde für eine breite Auswahl von Browsern und Geräten geprüft.

Weitere wichtige Informationen zu TLS finden Sie unter [TLS-Verschlüsselungsänderungen (Transport Layer Security](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standard/Premium-Benutzeroberfläche

Die [!DNL Target]-Schnittstelle unterstützt die folgenden Browser und Geräte:

>[!NOTE]
>
>Target unterstützt die neueste Version jedes aufgelisteten Browsers und die neueste Version abzüglich 1.


| Gerätetyp | Browser-Version |
|--- |--- |
| [!DNL Windows] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |
| [!DNL Mac] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |

## Anforderungen an die visuelle Bearbeitung

Damit Sie Ihre Web-Seiten zuverlässig im [!UICONTROL Visual Experience Composer] (VEC) öffnen, erstellen und in der Vorschau anzeigen können, muss die Browser-Erweiterung [Adobe Experience Cloud Visual Editing Helper](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank} in Ihrem Webbrowser installiert sein oder [!UICONTROL Enhanced Experience Composer (EEC)] verwenden.

>[!NOTE]
>
>[!DNL Google Chrome] und [!DNL Microsoft Edge] sind derzeit die einzigen Browser, die die visuelle Bearbeitung von Web-Seiten in [!DNL Adobe Target] unterstützen.


## Inhaltsbereitstellung

Die Inhaltsbereitstellung wurde für folgende Browser und Geräte getestet:

| Gerätetyp | Browser-Version |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 und 10. Im Emulationsmodus getestet. **Hinweis**: Die Inhaltsbereitstellung auf IE 9 wird von at.js 1.3.0 (und höher) nicht mehr unterstützt. Die Inhaltsbereitstellung auf IE 10, 11 und allen älteren Versionen wird von at.js 2.5.0 (und höher) nicht mehr unterstützt.</li><li>Internet Explorer 11. **Hinweis**: Die Inhaltsbereitstellung auf IE 10, 11 und allen älteren Versionen wird von at.js 2.5.0 (und höher) nicht mehr unterstützt.</li><li>Microsoft Edge</li><li>Chrome (aktuelle, neueste minus 1)</li><li>Firefox (neueste, neueste minus 1)</li></ul> |
| Mac | <ul><li>Apple Safari (aktuelle). **Hinweis**: Weitere Informationen dazu, wie Safari Erstanbieter- und Drittanbieter-Cookies verarbeitet, finden Sie unter [Target-Cookie](../implement/client-side/atjs/atjs-cookies.md).</li><li>Firefox (neueste, neueste minus 1)</li><li>Chrome (aktuelle, neueste minus 1)</li></ul> |
| Mobiltelefon/Tablet | <ul><li>Apple iOS (aktuelle)</li><li>Android-Geräte und -Tablets (Android 4 und neuer)</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

Beachten Sie Folgendes:

* Die [!DNL Adobe Experience Platform Web SDK] wurde für eine optimale Funktionsweise in den neuesten Versionen von [!DNL Google Chrome], [!DNL Safari], [!DNL Firefox] und [!DNL Microsoft Edge Chromium] entwickelt. Bei der Verwendung bestimmter Funktionen in älteren Versionen dieser Browser oder veralteten Browsern, wie z. B. [!DNL Internet Explorer], können Probleme auftreten.
* Bei at.js-Implementierungen zeigt [!DNL Target] Standardinhalte in früheren Versionen von Internet Explorer und möglicherweise in früheren Versionen der oben aufgeführten Browser an.
* In Internet Explorer werden alle unbekannten Elemente (z. B. benutzerdefinierte Elemente) als derselbe Elementtyp behandelt. Daher funktioniert der Versand nicht mit benutzerdefinierten Elementen.
* [!DNL Target] zeigt Standardinhalte in Browsern an, die oben nicht aufgeführt sind, und in Browsern, die den [Quirks-Modus“ ](https://en.wikipedia.org/wiki/Quirks_mode). Für at.js ist ein Dokumenttyp erforderlich, der im Standardmodus dargestellt wird, beispielsweise `<!DOCTYPE html>`.
* [!DNL Adobe] Bereitstellungsinfrastruktur wird nach dem 12. September 2018 so gesichert, dass TLS 1.0-Geräte und -Browser NICHT mehr unterstützt werden. Siehe [Änderungen hinsichtlich der Verschlüsselung mit TLS (Transport Layer Security)](../before-implement/tls-transport-layer-security-encryption.md), um die Gesamtauswirkungen dieser Änderung zu verstehen.
