---
description: Erfahren Sie, wie Sie mit dem  [!DNL Adobe Mobile SDK]  die optimalen Erlebnisse für Ihre Besucher Ihrer mobilen App anzeigen können.
title: Wie funktioniert [!DNL Target] in mobilen Apps?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 17%

---

# Funktionsweise von [!DNL Target] in Apps

Der [!DNL Adobe Mobile SDK] kontaktiert den [!DNL Target] -Server, um den Inhalt zusammen mit anderen Datenpunkten abzurufen und dem Benutzer das richtige Erlebnis anzuzeigen.

>[!IMPORTANT]
>
>Unterstützung für Version 4 von [!DNL Adobe Mobile].*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr für [!DNL Adobe Target] Mobilbenutzer empfohlen.
>
>Das [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Unterstützung von [!DNL Adobe Experience Cloud] -Lösungen und -Diensten in Ihren mobilen Apps.

## [!DNL Target] Orte und Erfolgsmetriken

Ein *Zielort* wird auch als Mbox bezeichnet. Ein in der Anwendung identifizierter Ort wird für Tests oder Personalisierung aktiviert (beispielsweise die Willkommensnachricht auf dem Starbildschirm). Diese Orte werden während der Testerstellung festgelegt.

Eine *[Erfolgsmetrik](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)* ist eine Aktion, die vom Benutzer ausgeführt wird und in der festgestellt wird, ob eine bestimmte Aktivität erfolgreich war (z. B. Anmeldung, Kauf, Buchung eines Tickets usw.).

![alt image](assets/mobile-target-location.png)

* **[!DNL Target]location:** Der Inhalt, der unter der Registerschaltfläche angezeigt wird.

  Diesem Benutzer wird beispielsweise kostenloser Versand bis 18:00 Uhr angeboten. Dieser Ort kann für mehrere [!DNL Target] -Aktivitäten wiederverwendet werden, um A/B-Tests und Personalisierungen durchzuführen.

* **Erfolgsmetrik:** Die vom Benutzer ausgeführte Aktion, bei der der Benutzer auf die Registrierungsschaltfläche tippt.

**So funktioniert [!DNL Target] im SDK**

![alt image](assets/how-target-mobile-works.png)
