---
description: Erfahren Sie, wie Sie mit  [!DNL Adobe Mobile SDK]  die optimalen Erlebnisse für Besucher Ihrer Mobile App anzeigen können.
title: Wie funktioniert  [!DNL Target]  in Mobile Apps?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 17%

---

# Funktionsweise von [!DNL Target] in Mobile Apps

Der [!DNL Adobe Mobile SDK] kontaktiert den [!DNL Target]-Server, um den Inhalt zusammen mit anderen Datenpunkten abzurufen, um dem Benutzer das richtige Erlebnis zu zeigen.

>[!IMPORTANT]
>
>Unterstützung für die [!DNL Adobe Mobile] Version 4.*x* SDKs sind seit dem 31. August 2021 ausgelaufen und werden für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

## [!DNL Target] und Erfolgsmetriken

Ein *Zielspeicherort* wird auch als Mbox bezeichnet. Ein in der Anwendung identifizierter Ort wird für Tests oder Personalisierung aktiviert (beispielsweise die Willkommensnachricht auf dem Starbildschirm). Diese Orte werden während der Testerstellung festgelegt.

Eine *[Erfolgsmetrik](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=de)* ist eine vom Benutzer durchgeführte Aktion, die angibt, ob eine bestimmte Aktivität erfolgreich war (z. B. Anmeldung, Kauf, Buchung eines Tickets usw.).

![ALT-Bild](assets/mobile-target-location.png)

* **[!DNL Target]:** Der Inhalt, der unter der Schaltfläche Registrieren angezeigt wird.

  Diesem Benutzer wird beispielsweise kostenloser Versand bis 18:00 Uhr angeboten. Dieser Speicherort kann über mehrere [!DNL Target] hinweg wiederverwendet werden, um A/B-Tests und Personalisierungen durchzuführen.

* **Erfolgsmetrik:** Die Aktion, die vom Benutzer an der Stelle ausgeführt wird, an der der Benutzer auf die Schaltfläche „Registrieren“ tippt.

**So funktioniert [!DNL Target] in SDK**

![ALT-Bild](assets/how-target-mobile-works.png)
