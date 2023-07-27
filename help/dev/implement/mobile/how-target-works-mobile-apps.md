---
description: Erfahren Sie, wie Sie die [!DNL Adobe Mobile SDK] , um den Besuchern Ihrer App die optimalen Erlebnisse anzuzeigen.
title: Funktionsweise [!DNL Target] Arbeiten Sie in mobilen Apps?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 34%

---

# How [!DNL Target] funktioniert in Apps

Die [!DNL Adobe Mobile SDK] kontaktieren [!DNL Target] -Server, um den Inhalt zusammen mit anderen Datenpunkten abzurufen und dem Benutzer das richtige Erlebnis anzuzeigen.

>[!IMPORTANT]
>
>Unterstützung für [!DNL Adobe Mobile] Version 4.*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr empfohlen für [!DNL Adobe Target] Mobilbenutzer.
>
>Die [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Stromversorgung [!DNL Adobe Experience Cloud] Lösungen und Dienste in Ihren mobilen Apps.

## [!DNL Target] Orte und Erfolgsmetriken

Ein *Zielort* wird auch wie folgt genannt:  mbox. Ein in der Anwendung identifizierter Ort wird für Tests oder Personalisierung aktiviert (beispielsweise die Willkommensnachricht auf dem Starbildschirm). Diese Orte werden während der Testerstellung festgelegt.

A *[Erfolgsmetrik](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* ist eine Aktion, die vom Benutzer ausgeführt wird und zeigt, dass eine bestimmte Aktivität von Erfolg gekrönt war (beispielsweise Registrierung, Absenden einer Bestellung, Buchung eines Tickets usw.).

![ALT-Bild](assets/mobile-target-location.png)

* **[!DNL Target]location:** Der Inhalt, der unter der Registrierungsschaltfläche angezeigt wird.

  Diesem Benutzer wird beispielsweise kostenloser Versand bis 18:00 Uhr angeboten. Dieser Speicherort kann über mehrere [!DNL Target] Aktivitäten zur Durchführung von A/B-Tests und Personalisierungen.

* **Erfolgsmetrik:** Die vom Benutzer ausgeführte Aktion, wenn der Benutzer auf die Registrierungsschaltfläche tippt.

**Grundlegendes zur [!DNL Target] funktioniert im SDK**

![ALT-Bild](assets/how-target-mobile-works.png)
