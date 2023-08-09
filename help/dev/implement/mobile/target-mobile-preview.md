---
keywords: QS, Vorschau, Vorschau-Link, Mobile, mobile Vorschau
description: Verwenden Sie Vorschaulinks für Mobilgeräte, um eine durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen. Sie können sich ohne spezielle Testgeräte für verschiedene Erlebnisse anmelden.
title: Wie verwende ich den Vorschau-Link für Mobilgeräte in [!DNL Target] Mobil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 97c96e63f9121793a83b445ad3dc33c5d094509a
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 51%

---

# [!DNL Target] mobile preview

Verwenden Sie die Vorschau für mobile Apps, um mühelos eine ganzheitliche Qualitätssicherung für Aktivitäten von mobilen Apps durchzuführen und sich ohne spezielle Prüfmittel direkt auf Ihrem Gerät für verschiedene Erlebnisse anzumelden.

## Überblick

Mit der mobilen Vorschaufunktionalität können Sie Aktivitäten in Ihrer mobilen App vollständig testen, bevor Sie sie live schalten.

## Voraussetzungen 

1. **Verwenden Sie eine unterstützte Version des SDK:** Für die mobile Vorschaufunktion müssen Sie die entsprechende Version des Adobe Mobile SDK in Ihre entsprechenden Apps herunterladen und installieren.

   Anweisungen zum Herunterladen des entsprechenden SDK finden Sie unter [Aktuelle SDK-Versionen](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} im *[!DNL Adobe Experience Platform Mobile SDK]* Dokumentation.

1. **URL-Schema einrichten:** Der Vorschau-Link öffnet Ihre App über ein URL-Schema. Sie müssen ein einzigartiges URL-Schema für die Vorschau festlegen.

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* im *[!DNL Adobe Experience Platform Mobile SDK]* Dokumentation.

   Die folgenden Links enthalten weitere Informationen:

   * **iOS**: Weitere Informationen zum Festlegen von URL-Schemas für iOS finden Sie unter [Definieren eines benutzerdefinierten URL-Schemas für Ihre App](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} auf der Apple Developer-Website.
   * **Android**: Weitere Informationen zum Festlegen von URL-Schemas für Android finden Sie unter [Erstellen von Deep-Links zu App-Inhalten](https://developer.android.com/training/app-links/deep-linking){target=_blank} auf der Android Developers-Website.

1. **Einrichten `collectLaunchInfo` API (nur i0S)**

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Adobe Target* im *[!DNL Adobe Experience Platform Mobile SDK]* Dokumentation.

## Einen Vorschau-Link erstellen

1. Im [!DNL Target] Klicken Sie in der Benutzeroberfläche auf **[!UICONTROL Weitere Optionen]** Symbol (die vertikale Ellipse), und wählen Sie **[!UICONTROL Mobile Vorschau erstellen]**.

   ![ALT-Bild](assets/mobile-preview-create.png)

1. Wählen Sie die Aktivitäten aus, die Sie in der Vorschau anzeigen möchten, und klicken Sie auf **[!UICONTROL Link zur mobilen Vorschau erstellen]**.

   >[!NOTE]
   >
   >Es können nur formularbasierte AB- und XT-Aktivitäten ausgewählt werden.

   ![ALT-Bild](assets/mobile-preview-select-activities.png)

1. Legen Sie das URL-Schema Ihrer App fest.

   Dieses muss dem Schema in Ihrer iOS- oder Android-App entsprechen. Wiederholen Sie diesen Vorgang bei Bedarf einzeln für iOS und Android.

   ![ALT-Bild](assets/mobile-preview-enter-url-scheme.png)

1. Klicken Sie auf **[!UICONTROL Vorschaulink für Mobilversion erzeugen]** und kopieren Sie den Link.

   ![ALT-Bild](assets/mobile-preview-generate-and-copy.png)

## Vorschau auf Ihrem Gerät

Öffnen Sie den Link in einem mobilen Browser auf einem Gerät, auf dem Ihre App installiert ist. Bei dieser App kann es sich um die aus dem Apple App Store oder dem Google Play Store heruntergeladene Produktions-App handeln. Es muss keine speziell erstellte Version sein. Wenn Sie einen aktiven Vorschaulink haben, können Sie über das Gerät auf die Erlebnisse zugreifen.

1. Öffnen Sie den Link in Ihrem mobilen Browser.

   Geben Sie den Link frei, den Sie im vorherigen Schritt aus dem [!DNL Target] Benutzeroberflächen auf Ihrem Mobilgerät auf bequeme Weise, z. B. durch die Verwendung von Text, E-Mail oder Slack.

   |![Vorschau Deep Link 1](assets/mobile-preview-open-deeplink.png)|![Vorschau Deep Link 2](assets/mobile-preview-open-app.png)|

   Ihre App wird geöffnet und startet [!DNL Target] Mobile Vorschaumodus.

1. Wählen Sie die Kombination aus Erlebnissen aus, die Sie sehen möchten, und klicken Sie auf **[!UICONTROL Erlebnisse starten]**.

   |![mobile preview 1](assets/mobile-preview-experience-selection-1.png)|![mobile Vorschau 2](assets/mobile-preview-experience-result-1-france.png)|![mobile Vorschau 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![mobile Vorschau 4](assets/mobile-preview-experience-selection-2.png)|![mobile Vorschau 5](assets/mobile-preview-experience-result-2-aus.png)|![mobile Vorschau 6](assets/mobile-preview-experience-result-2-10off.png)|

## Einschränkungen  

* Die Ansicht muss erneut laden, damit der neue Inhalt angezeigt werden kann, nachdem die Schaltfläche **[!UICONTROL Erlebnisse starten]** aktiviert wurde. Die einfachste Möglichkeit ist, zu einem anderen Bildschirm zu wechseln und danach zu dem Bildschirm zurückzukehren, auf dem die Änderung bewirkt werden soll.
* Die mobile Vorschau wird nicht für frühere Android-Versionen als API-19 (KitKat) unterstützt.
