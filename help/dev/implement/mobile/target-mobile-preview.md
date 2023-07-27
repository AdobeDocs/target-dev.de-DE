---
keywords: QS, Vorschau, Vorschau-Link, Mobile, mobile Vorschau
description: Verwenden Sie Vorschaulinks für Mobilgeräte, um eine durchgängige Qualitätssicherung für Aktivitäten mobiler Apps durchzuführen. Sie können sich ohne spezielle Testgeräte für verschiedene Erlebnisse anmelden.
title: Wie verwende ich den Vorschau-Link für Mobilgeräte in [!DNL Target] Mobil?
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 68%

---

# [!DNL Target] mobile preview

Verwenden Sie die Vorschau für mobile Apps, um mühelos eine ganzheitliche Qualitätssicherung für Aktivitäten von mobilen Apps durchzuführen und sich ohne spezielle Prüfmittel direkt auf Ihrem Gerät für verschiedene Erlebnisse anzumelden.

>[!NOTE]
>
>Für die Vorschaufunktion für die Mobilversion ist es erforderlich, dass Sie die entsprechende Version 4.14 (oder später) des Adobe Mobile-SDK herunterladen und installieren.

## Überblick

Mit der mobilen Vorschaufunktionalität können Sie Aktivitäten in Ihrer mobilen App vollständig testen, bevor Sie sie live schalten.

## Voraussetzungen 

1. **Verwenden Sie eine unterstützte Version des SDK:** Für die mobile Vorschaufunktion ist es erforderlich, dass Sie die entsprechende Version 4.14 (oder später) des Adobe Mobile-SDK in Ihren jeweiligen Apps herunterladen.

   Eine Anleitung zum Herunterladen des erforderlichen SDK finden Sie unter:

   * **iOS:** [Vorbereitung](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/requirements.html) im *Hilfe zu Mobile Services iOS*.
   * **Android:** [Vorbereitung](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html) im *Hilfe zu Mobile Services für Android*.

1. **URL-Schema einrichten:** Der Vorschau-Link öffnet Ihre App über ein URL-Schema. Sie müssen ein einzigartiges URL-Schema für die Vorschau festlegen.

   Die folgende Illustration stellt ein Beispiel unter iOS dar:

   ![ALT-Bild](assets/mobile-preview-url-scheme-ios.png)

   Die folgende Illustration stellt ein Beispiel unter Android dar:

   ![ALT-Bild](assets/Android_Deeplink.png)

1. **Adobe DeepLink verfolgen**

   **iOS:** Rufen Sie in App Delegate `[ADBMobile trackAdobeDeepLink:url` auf, wenn der Delegate dazu aufgefordert wird, die Ressource mit dem URL-Schema zu öffnen, das im vorherigen Schritt angegeben wurde.

   Das folgende Code-Snippet dient als Beispiel:

   ```javascript {line-numbers="true"}
   - (BOOL) application:(UIApplication *)app openURL:(NSURL *)url 
                options:(NSDictionary<NSString *,id> *)options { 
   
       if ([[url scheme] isEqualToString:@"com.adobe.targetmobile"]) { 
           [ADBMobile trackAdobeDeepLink:url]; 
           return YES; 
       } 
       return NO; 
   } 
   ```

   **Android:** Rufen Sie in der App `Config.trackAdobeDeepLink(URL);` auf, wenn der Aufrufende dazu aufgefordert wird, die Ressource mit dem URL-Schema zu öffnen, das im vorherigen Schritt angegeben wurde.

   ```javascript {line-numbers="true"}
    private Boolean shouldOpenDeeplinkUrl() { 
        Intent appLinkIntent = getIntent(); 
        String appLinkAction = appLinkIntent.getAction(); 
        Uri appLinkData = appLinkIntent.getData; 
        if (appLinkData.toString().startsWith("com.adobe.targetmobile")) { 
            Config.trackAdobeDeepLink(appLinkData); 
            return true; 
        } 
        return false; 
     }
   ```

   Damit die Mobile-Vorschau für Android funktioniert, müssen Sie außerdem das folgende Codefragment in AndroidManifest.xml hinzufügen, wenn Sie Version 5 des Adobe Mobile SDK verwenden:

   ```javascript {line-numbers="true"}
   <activity android:name="com.adobe.marketing.mobile.FullscreenMessageActivity" />
   ```

   Wenn Sie Version 4 des Adobe Mobile SDK verwenden, verwenden Sie folgendes Codefragment:

   ```javascript {line-numbers="true"}
   <activity android:name="com.adobe.mobile.MessageFullScreenActivity" />
   ```

## Einen Vorschau-Link erstellen

1. Im [!DNL Target] Klicken Sie in der Benutzeroberfläche auf **[!UICONTROL Weitere Optionen]** Symbol (drei vertikale Ellipsen), und wählen Sie **[!UICONTROL Mobile Vorschau erstellen]**.

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
