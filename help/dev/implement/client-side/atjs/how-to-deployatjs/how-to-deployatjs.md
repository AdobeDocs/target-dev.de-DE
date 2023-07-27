---
keywords: Implementierung, at.js, JavaScript-Bibliothek
description: Erfahren Sie, wie Sie die [!DNL Adobe Target]  JavaScript-Bibliothek "at.js"mit Tags in [!DNL Adobe Experience Platform] oder ohne Tag-Manager.
title: Wie stelle ich at.js bereit?
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 27%

---

# Bereitstellen von „at.js“

Informationen zur Bereitstellung der [!DNL Adobe Target]  JavaScript-Bibliothek, at.js, mithilfe von Tags in [!DNL Adobe Experience Platform] oder ohne Tag-Manager.

Sie können at.js mithilfe der folgenden Methoden bereitstellen:

* **[Implementierung [!DNL Target] Verwenden von Tags in Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)**: Tags in [!DNL Adobe Experience Platform] sind die nächste Generation von Tag-Management-Funktionen von Adobe. Launch bietet Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die zur Unterstützung entsprechender Kundenerlebnisse erforderlich sind.

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] wurde als Suite von Datenerfassungstechnologien in [!DNL Adobe Experience Platform] umbenannt. Dies spiegelt sich in der Produktdokumentation in verschiedenen Änderungen hinsichtlich der verwendeten Begriffe wider. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html).

* **[Implementierung [!DNL Target] ohne Tag-Manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)**: Sie können [!DNL Target] ohne Verwendung eines Tag-Managers (z. B. Tags in [!DNL Adobe Experience Platform]).
* **Implementierung [!DNL Target] Verwendung eines Drittanbieter-Tag-Managers**: [Tags in Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) die bevorzugte Methode zur Implementierung von [!DNL Target]Sie können jedoch auch [!DNL Target] Verwendung eines Drittanbieter-Tag-Managers, einschließlich Tealium, Ensighten und Google-Tag. Eine Liste der Vorteile der Verwendung von Launch finden Sie unter [Vorteile der Implementierung von at.js mithilfe der [!DNL Adobe Target]  Erweiterung](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension).

  Wenn Sie jedoch wissen, wie [!DNL Target] ohne Tag-Manager können Sie mühelos mit einem Drittanbieter-Tag-Manager implementieren, anstatt at.js im Site-Code fest zu codieren.

  Im Folgenden finden Sie zwei wichtige Themen, die Sie bei der Implementierung unterstützen [!DNL Target] mit einem Drittanbieter-Tag-Manager:

   * [Vor der Implementierung](/help/dev/before-implement/prepare-to-implement-target.md)
   * [Implementierung [!DNL Target] ohne Tag-Manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  Weitere Informationen finden Sie in der Dokumentation für Ihren Drittanbieter-Tag-Manager.

Zu implementieren [!DNL Target] bei Verwendung von Einzelseiten-Apps (SPA) siehe [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).
