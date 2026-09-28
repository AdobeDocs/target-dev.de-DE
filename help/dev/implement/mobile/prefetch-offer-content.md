---
keywords: Angebot, Vorabruf, iOS, Android, SDK, Mobile, Mobile SDK, 8 $
description: Verwenden Sie die [!DNL Adobe Target]-Vorabruf-Funktion in den iOS- und Android Mobile-SDKs, um Angebotsinhalte durch Zwischenspeichern der Serverantworten so oft wie möglich abzurufen.
title: Kann ich Angebotsinhalte für Mobile Apps im Voraus abrufen?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 37%
---
# Vorabruf des Angebotsinhalts

Die [!DNL Target] Vorabruffunktion verwendet die iOS- und Android Mobile-SDKs, um so wenige Angebotsinhalte wie möglich abzurufen, indem sie die Serverantworten zwischenspeichert.

>[!IMPORTANT]
>
>Die Unterstützung für die [!DNL Adobe Mobile] Version 4.*x*-SDKs endete am 31. August 2021 und wird für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

Dieser Prozess reduziert die Ladezeit, verhindert multiple Netzwerkaufrufe und ermöglicht es [!DNL Target], darüber benachrichtigt zu werden, welche Mbox vom Benutzer der mobilen Anwendung besucht wurde. Der gesamte Inhalt wird abgerufen und während des Aufrufs für den Vorabruf im Cache abgelegt, und dieser Inhalt wird bei allen zukünftigen Aufrufen abgerufen, die im Cache abgelegte Inhalte für den spezifizierten mbox-Namen enthalten.

Beachten Sie die folgenden Einschränkungen bei der Verwendung der Prefetch-Methode mit den iOS- und Android Mobile-SDKs:

* Vorabgerufene Inhalte werden nicht über Starts hinweg behalten. Der Inhalt des vorherigen Artikels wird zwischengespeichert, solange die Anwendung aktiv ist oder bis die `clearPrefetchCache()` Methode aufgerufen wird.
* Die Vorabruf-Funktion wird nicht unterstützt für [!UICONTROL Automatische Zuordnung] und [!UICONTROL Automatisches Targeting] Traffic-Zuordnungsmethoden, für [!UICONTROL Automated Personalization] oder [!UICONTROL Recommendations]-Aktivitätstypen oder für [Recommendations-Angebote innerhalb einer A/B- oder XT-Aktivität](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

Weitere Informationen einschließlich Vorabruf-Methoden, öffentliche Klassen und Code-Beispiele finden Sie unter:

* **iOS:** [Vorab-Abrufen von Angebotsinhalten in iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) in der *Mobile Services iOS SDK-Hilfe*.
* **Android:** [Vorab-Abrufen von Angebotsinhalten in Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) in der *Mobile Services Android SDK-Hilfe*.
