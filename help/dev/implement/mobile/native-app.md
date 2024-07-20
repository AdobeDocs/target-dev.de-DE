---
keywords: mobile app,aep sdk,native app,web views,native;swift,adobe experience platform mobile sdk,mobile sdk,nativer Code
description: Erfahren Sie, wie Sie [!DNL Adobe Target] mit dem [!DNL AEP Mobile SDK]  in eine native App mit Webansichten implementieren.
title: Implementieren von [!DNL Adobe Target] in eine mobile App, die nativen Code mit Webansichten verwendet
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Implementieren von [!DNL Target] mit dem [!DNL AEP Mobile SDK] in einer nativen App mit Webansichten

In diesem Artikel werden Best Practices für die Implementierung von [!DNL Adobe Target] in einer mobilen App vorgestellt, die nativen Code mit Webansichten verwendet, die die [!DNL Adobe Experience Platform Mobile SDK] verwenden.

In diesem Artikel wird eine iOS-Beispielanwendung mit dem Code [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} und einer Integration mit dem Namen [!DNL Target] verwendet, die in [Swift aus dem GitHub-Repository geschrieben wurden](https://github.com/adobe/aep-sdk-app/){target=_blank}.

In der realen Welt verwendet Ihre Enterprise-App wahrscheinlich Webansichten in Ihrer mobilen App. Eine Webansicht ist ein Container, der eine Webseite mithilfe einer URL lädt. Der Container ähnelt einem Browserfenster ohne Steuerelemente. In iOS funktioniert der Webansichtsbehälter bei der Verarbeitung von Webseiten als Safari-Browser.

## Voraussetzungen 

Um mit dem [!DNL Adobe Experience Platform Mobile SDK] beginnen zu können, müssen Sie einige vorbereitende Aufgaben ausführen.

Weitere Informationen finden Sie unter [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in der Dokumentation zu [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Synchronisieren von nativem Code mit Webansichten

Die Herausforderung bei der Implementierung von [!DNL Target] in einer nativen App mit Webansichten besteht darin, dass die [!DNL Adobe Experience Platform Mobile SDK] bereits alle erforderlichen Kennungen generiert hat, damit [!DNL Adobe] -Lösungen reibungslos funktionieren. Die Identifikatoren sind jedoch noch nicht für die Webansichten sichtbar, da sie sich nicht in der nativen Plattformumgebung befinden. Daher müssen Sie eine Verbindung erstellen, um einige SDK-IDs an die Webansichten zu übergeben, damit die Besucheridentität in der Webumgebung erhalten bleibt. Andernfalls werden doppelte Besuche ausgegeben, was sich auf Ihre Berichterstellung auswirkt.

Glücklicherweise bietet der [!DNL Adobe Experience Platform Mobile SDK] eine praktische Methode zum Generieren von [!DNL Adobe] -Parametern, die erforderlich sind, damit Webansichten denselben Besucher nutzen und beibehalten können, wie im folgenden Beispielcode dargestellt:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

Weitere Informationen zur `Identity.appendTo` -Methode und ein Beispiel für die Verwendung der -Methode finden Sie unter [Swift > Beispiel](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} in der *Mobile SDK-Dokumentation*.

Mithilfe von `Identity.appendTo`, diese URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

wird in:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Wie Sie sehen können, wird der Parameter `adobe_mc` an die URL angehängt. Dieser Parameter enthält kodierte Werte für:

* TS=1660667205: Der aktuelle Zeitstempel. Dieser Zeitstempel stellt sicher, dass die Webansicht keine abgelaufenen Werte erhält.
* MCMID=69624092487065093697422606480535692677: Die [!UICONTROL Experience Cloud ID] (ECID). Wird auch als MID oder [!UICONTROL Marketing Cloud ID] bezeichnet, die für die lösungsübergreifende Besucheridentifizierung mit [!DNL Adobe] erforderlich ist.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: Die [!UICONTROL Adobe Organization ID].

Die `Identity.getUrlVariables` ist eine alternative [!DNL Adobe Experience Platform Mobile SDK] -Methode, die eine entsprechend geformte Zeichenfolge zurückgibt, die die [!DNL Experience Cloud Identity Service]-URL-Variablen enthält. Weitere Informationen finden Sie unter [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} in der *Identitäts-API-Referenz*.

## Übergeben der [!DNL Target] Sitzungs-ID für das Erlebnis derselben Sitzung

Ein weiterer Schritt ist erforderlich, damit die [!DNL Target]-Benutzer-Journey nahtlos über die nativen und Web-Ansichten hinweg funktioniert. Dieser Schritt umfasst das Extrahieren und Übergeben der [!DNL Target] Sitzungs-ID aus dem [!DNL Adobe Experience Platform Mobile SDK] an die Webansichten der mobilen App.

Der `Target.getSessionId` extrahiert die Sitzungs-ID, die als `mboxSession` -Parameter an die Webansichts-URL übergeben werden kann:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testen in Webansichten

Webvorschau-Links werden auf der Seite &quot;[!UICONTROL Activity detail]&quot;generiert, indem Sie auf den Link &quot;[[!UICONTROL Adobe QA]&quot;](/help/dev/implement/mobile/target-mobile-preview.md) klicken, um ein Popup anzuzeigen und jeden Erlebnisvorschau-Link zu kopieren. Dies ähnelt dem folgenden Beispiel:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Webvorschau-Links enthalten zusätzliche Parameter `at_preview_index` und `at_preview_listed_activities_only`. Kopieren Sie diese Parameter, um mobile Vorschaulinks mit Weblink-Parametern zu erstellen.

Beispiel:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Nach dem Öffnen des Links in einem iOS Safari-Browser erfasst Ihre App die URL in Ihrer `AppDelegate` -Klasse ähnlich dem folgenden Beispiel:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Nachdem Sie alle erforderlichen Parameter in der App erfasst haben, können Sie sie bei Bedarf an das Internet übergeben:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

Die endgültige Ausgabe des Webansichts-Links könnte wie folgt aussehen:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
