---
keywords: QS, Vorschau, Vorschau-Link, Mobile, mobile Vorschau
description: Verwenden Sie Vorschaulinks für Mobilgeräte, um eine durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen.
title: Wie verwende ich mobile Vorschaulinks in [!DNL Adobe Target] Mobile?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# [!DNL Target] mobile Vorschau

Verwenden Sie Vorschaulinks für Mobilgeräte, um eine einfache durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen und sich ohne spezielle Testgeräte bei verschiedenen Erlebnissen auf Ihrem Gerät anzumelden.

Mit der mobilen Vorschaufunktion können Sie die Aktivitäten Ihrer Mobile App vollständig testen, bevor Sie sie live schalten.

## Voraussetzungen 

1. **Verwenden Sie eine unterstützte Version des SDK:** Für die Vorschaufunktion für Mobilgeräte müssen Sie die entsprechende Version von [!DNL Adobe Mobile SDK] in Ihre entsprechenden Apps herunterladen und installieren.

   Anweisungen zum Herunterladen des entsprechenden SDK finden Sie unter [Aktuelle SDK-Versionen](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} in der *[!DNL Adobe Experience Platform Mobile SDK]* -Dokumentation.

1. **URL-Schema einrichten:** Der Vorschau-Link öffnet Ihre App über ein URL-Schema. Geben Sie ein eindeutiges URL-Schema für die Vorschau an.

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Konfigurieren der Target-Erweiterung in der Data Connection-Benutzeroberfläche* in der Dokumentation zu *[!DNL Mobile SDK]*.

   Die folgenden Links enthalten weitere Informationen:

   * **iOS**: Weitere Informationen zum Festlegen von URL-Schemas für iOS finden Sie unter [Definieren eines benutzerdefinierten URL-Schemas für Ihre App](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} auf der Website *Apple Developer* .
   * **Android**: Weitere Informationen zum Festlegen von URL-Schemas für Android finden Sie unter [Erstellen von Deep-Links zu App-Inhalten](https://developer.android.com/training/app-links/deep-linking){target=_blank} auf der Website *Android-Entwickler* .

1. **Richten Sie die `collectLaunchInfo`-API ein (nur i0S)**

   Weitere Informationen finden Sie unter [Visuelle Vorschau](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} in *Konfigurieren der Target-Erweiterung in der Data Connection-Benutzeroberfläche* in der Dokumentation zu *[!DNL Mobile SDK]*.

## Einen Vorschau-Link erstellen

1. Klicken Sie in der Benutzeroberfläche von [!DNL Target] auf das Symbol **[!UICONTROL More Options]** (die vertikale Ellipse) und wählen Sie dann **[!UICONTROL Create Mobile Preview Link]** aus.

   ![alt image](assets/mobile-preview-create.png)

1. Wählen Sie die Aktivitäten aus, die Sie in der Vorschau anzeigen möchten, und klicken Sie dann auf **[!UICONTROL Generate Mobile Preview Link]**.

   >[!NOTE]
   >
   >Sie können nur formularbasierte [!UICONTROL A/B Test] - und [!UICONTROL Experience Targeting] -Aktivitäten (XT) auswählen.

   ![alt image](assets/mobile-preview-select-activities.png)

1. Legen Sie das URL-Schema Ihrer App fest.

   Das URL-Schema muss mit dem in Ihrer iOS- oder Android-App vorhandenen übereinstimmen. Wiederholen Sie diesen Vorgang bei Bedarf für iOS und Android separat.

   ![alt image](assets/mobile-preview-enter-url-scheme.png)

1. Klicken Sie auf **[!UICONTROL Generate Mobile Preview Link]** und kopieren Sie dann den Link.

   ![alt image](assets/mobile-preview-generate-and-copy.png)

## Vorschau auf Ihrem Gerät

Öffnen Sie den Link in einem mobilen Browser auf einem Gerät, auf dem Ihre App installiert ist. Bei dieser App kann es sich um die Produktions-App handeln, die Sie vom [!DNL Apple App Store] oder vom [!DNL Google Play Store] heruntergeladen haben. Die App muss kein spezieller Build sein. Wenn Sie über einen aktiven Vorschau-Link verfügen, können Sie die Erlebnisse auf dem Gerät anzeigen.

1. Öffnen Sie den Link in Ihrem mobilen Browser.

   Geben Sie den Link, den Sie im vorherigen Abschnitt aus der Benutzeroberfläche von [!DNL Target] kopiert haben, auf Ihrem Mobilgerät frei, z. B. mithilfe von Text, E-Mail oder [!DNL Slack].

   |![Vorschau Deep Link 1](assets/mobile-preview-open-deeplink.png)|![Vorschau Deep Link 2](assets/mobile-preview-open-app.png)|

   Ihre App wird geöffnet und startet den [!DNL Target] [!UICONTROL Mobile Preview Mode].

1. Wählen Sie die Kombination der Erlebnisse aus, die Sie sehen möchten, und klicken Sie dann auf **[!UICONTROL Launch Experiences]**.

   |![mobile preview 1](assets/mobile-preview-experience-selection-1.png)|![mobile Vorschau 2](assets/mobile-preview-experience-result-1-france.png)|![mobile Vorschau 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![mobile Vorschau 4](assets/mobile-preview-experience-selection-2.png)|![mobile Vorschau 5](assets/mobile-preview-experience-result-2-aus.png)|![mobile Vorschau 6](assets/mobile-preview-experience-result-2-10off.png)|

## Einschränkungen  

* Die Ansicht muss erneut geladen werden, damit der neue Inhalt angezeigt wird, nachdem auf die Schaltfläche **[!UICONTROL Launch Experiences]** geklickt wurde. Die einfachste Möglichkeit ist, zu einem anderen Bildschirm zu wechseln und danach zu dem Bildschirm zurückzukehren, auf dem die Änderung bewirkt werden soll.
* Die mobile Vorschau wird nicht für frühere Android-Versionen als API-19 (KitKat) unterstützt.
