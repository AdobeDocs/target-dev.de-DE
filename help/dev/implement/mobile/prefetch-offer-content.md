---
keywords: Angebot, Vorabruf, iOS, Android, SDK, Mobile, Mobile SDK, 8 USD
description: Verwenden Sie die Vorabruffunktion von  [!DNL Adobe Target] in den mobilen SDKs von iOS und Android , um so wenig Angebotsinhalte wie möglich abzurufen, indem Sie die Serverantworten zwischenspeichern.
title: Kann ich Angebotsinhalte für mobile Apps vorab abrufen?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Vorabruf des Angebotsinhalts

Die [!DNL Target] Vorabruffunktion verwendet die iOS- und Android Mobile-SDKs, um so wenige Angebotsinhalte wie möglich abzurufen, indem sie die Serverantworten zwischenspeichert.

>[!IMPORTANT]
>
>Unterstützung für Version 4 von [!DNL Adobe Mobile].*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr für [!DNL Adobe Target] Mobilbenutzer empfohlen.
>
>Das [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Unterstützung von [!DNL Adobe Experience Cloud] -Lösungen und -Diensten in Ihren mobilen Apps.

Dieser Prozess reduziert die Ladezeit, verhindert multiple Netzwerkaufrufe und ermöglicht es [!DNL Target], darüber benachrichtigt zu werden, welche Mbox vom Benutzer der mobilen Anwendung besucht wurde. Der gesamte Inhalt wird abgerufen und während des Aufrufs für den Vorabruf im Cache abgelegt, und dieser Inhalt wird bei allen zukünftigen Aufrufen abgerufen, die im Cache abgelegte Inhalte für den spezifizierten mbox-Namen enthalten.

Beachten Sie die folgenden Einschränkungen bei der Verwendung der Vorabruf-Methode mit den iOS- und Android Mobile SDKs:

* Vorabgerufene Inhalte werden nicht über Starts hinweg behalten. Der Inhalt des vorherigen Artikels wird zwischengespeichert, solange die Anwendung aktiv ist oder bis die `clearPrefetchCache()` Methode aufgerufen wird.
* Die Vorabruffunktion wird nicht für [!UICONTROL Auto-Allocate] - und [!UICONTROL Auto-Target] -Traffic-Zuordnungsmethoden, für [!UICONTROL Automated Personalization] - oder [!UICONTROL Recommendations] -Aktivitätstypen oder für [Empfehlungsangebote innerhalb einer A/B- oder XT-Aktivität](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html) unterstützt.

Weitere Informationen einschließlich Vorabruf-Methoden, öffentliche Klassen und Code-Beispiele finden Sie unter:

* **iOS:** [Vorabruf des Angebotsinhalts in iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) in der *Mobile Services iOS SDK-Hilfe*.
* **Android:** [Vorabruf des Angebotsinhalts in Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) in der *Mobile Services Android SDK-Hilfe*.
