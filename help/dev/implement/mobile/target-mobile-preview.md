---
keywords: QS, Vorschau, Vorschau-Link, Mobile, mobile Vorschau
description: Verwenden Sie Vorschaulinks für Mobilgeräte, um eine durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen.
title: Verwenden von mobilen Vorschaulinks in [!DNL Adobe Target] Mobil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 0bcfa16cb79644e7ce10e33daf6c8385104c197f
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 27%

---

# [!DNL Target] mobile preview

Verwenden Sie Vorschaulinks für Mobilgeräte, um eine einfache durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen und sich ohne spezielle Testgeräte bei verschiedenen Erlebnissen auf Ihrem Gerät anzumelden.

Mit der mobilen Vorschaufunktion können Sie die Aktivitäten Ihrer Mobile App vollständig testen, bevor Sie sie live schalten.

## Voraussetzungen 

1. **Verwenden Sie eine unterstützte Version des SDK:** Für die mobile Vorschaufunktion müssen Sie die entsprechende Version der [!DNL Adobe Mobile SDK] in den entsprechenden Apps.

   Anweisungen zum Herunterladen des entsprechenden SDK finden Sie unter [Aktuelle SDK-Versionen](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} im *[!DNL Adobe Experience Platform Mobile SDK]* Dokumentation.

1. **URL-Schema einrichten:** Der Vorschau-Link öffnet Ihre App über ein URL-Schema. Geben Sie ein eindeutiges URL-Schema für die Vorschau an.

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Konfigurieren der Target-Erweiterung in der Benutzeroberfläche &quot;Datenverbindung&quot;* im *[!DNL Mobile SDK]* Dokumentation.

   Die folgenden Links enthalten weitere Informationen:

   * **iOS**: Weitere Informationen zum Festlegen von URL-Schemas für iOS finden Sie unter [Definieren eines benutzerdefinierten URL-Schemas für Ihre App](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} auf *Apple-Entwickler* Website.
   * **Android**: Weitere Informationen zum Festlegen von URL-Schemas für Android finden Sie unter [Erstellen von Deep-Links zu App-Inhalten](https://developer.android.com/training/app-links/deep-linking){target=_blank} auf *Android-Entwickler* Website.

1. **Richten Sie die `collectLaunchInfo` API (nur i0S)**

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Konfigurieren der Target-Erweiterung in der Benutzeroberfläche &quot;Datenverbindung&quot;* im *[!DNL Mobile SDK]* Dokumentation.

## Einen Vorschau-Link erstellen

1. Im [!DNL Target] Klicken Sie in der Benutzeroberfläche auf **[!UICONTROL Weitere Optionen]** Symbol (die vertikale Ellipse), und wählen Sie **[!UICONTROL Link zur mobilen Vorschau erstellen]**.

   ![ALT-Bild](assets/mobile-preview-create.png)

1. Wählen Sie die Aktivitäten aus, die Sie in der Vorschau anzeigen möchten, und klicken Sie auf **[!UICONTROL Link zur mobilen Vorschau erstellen]**.

   >[!NOTE]
   >
   >Sie können nur formularbasierte Elemente auswählen [!UICONTROL A/B-Test] und [!UICONTROL Erlebnis-Targeting] (XT).

   ![ALT-Bild](assets/mobile-preview-select-activities.png)

1. Legen Sie das URL-Schema Ihrer App fest.

   Das URL-Schema muss mit dem in Ihrer iOS- oder Android-App vorhandenen identisch sein. Wiederholen Sie diesen Vorgang bei Bedarf für iOS und Android separat.

   ![ALT-Bild](assets/mobile-preview-enter-url-scheme.png)

1. Klicken Sie auf **[!UICONTROL Vorschaulink für Mobilversion erzeugen]** und kopieren Sie den Link.

   ![ALT-Bild](assets/mobile-preview-generate-and-copy.png)

## Vorschau auf Ihrem Gerät

Öffnen Sie den Link in einem mobilen Browser auf einem Gerät, auf dem Ihre App installiert ist. Diese App kann die Produktions-App sein, die Sie von der [!DNL Apple App Store] oder [!DNL Google Play Store]. Die App muss kein spezieller Build sein. Wenn Sie über einen aktiven Vorschau-Link verfügen, können Sie die Erlebnisse auf dem Gerät anzeigen.

1. Öffnen Sie den Link in Ihrem mobilen Browser.

   Geben Sie den Link frei, den Sie im vorherigen Abschnitt aus dem [!DNL Target] Benutzeroberflächen auf Ihrem Mobilgerät bequem bereitstellen, z. B. mit Text, E-Mail oder [!DNL Slack].

   |![Vorschau Deep Link 1](assets/mobile-preview-open-deeplink.png)|![Vorschau Deep Link 2](assets/mobile-preview-open-app.png)|

   Ihre App wird geöffnet und startet [!DNL Target] [!UICONTROL Mobile Vorschaumodus].

1. Wählen Sie die Kombination aus Erlebnissen aus, die Sie sehen möchten, und klicken Sie auf **[!UICONTROL Erlebnisse starten]**.

   |![mobile preview 1](assets/mobile-preview-experience-selection-1.png)|![mobile Vorschau 2](assets/mobile-preview-experience-result-1-france.png)|![mobile Vorschau 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![mobile Vorschau 4](assets/mobile-preview-experience-selection-2.png)|![mobile Vorschau 5](assets/mobile-preview-experience-result-2-aus.png)|![mobile Vorschau 6](assets/mobile-preview-experience-result-2-10off.png)|

## Einschränkungen  

* Die Ansicht muss erneut laden, damit der neue Inhalt angezeigt werden kann, nachdem die Schaltfläche **[!UICONTROL Erlebnisse starten]** aktiviert wurde. Die einfachste Möglichkeit ist, zu einem anderen Bildschirm zu wechseln und danach zu dem Bildschirm zurückzukehren, auf dem die Änderung bewirkt werden soll.
* Die mobile Vorschau wird nicht für frühere Android-Versionen als API-19 (KitKat) unterstützt.
