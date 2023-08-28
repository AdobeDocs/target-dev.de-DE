---
keywords: mobile app,aep sdk,native app,web views,native;swift,adobe experience platform mobile sdk,mobile sdk,nativer Code
description: Erfahren Sie, wie Sie [!DNL Adobe Target] mit dem [!DNL AEP Mobile SDK] in einer nativen App mit Webansichten.
title: Implementierung [!DNL Adobe Target] in einer mobilen App, die nativen Code mit Webansichten verwendet
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Implementierung [!DNL Target] mit dem [!DNL AEP Mobile SDK] in einer nativen App mit Webansichten

In diesem Artikel werden Best Practices für die Implementierung von [!DNL Adobe Target] in einer mobilen App, die nativen Code mit Webansichten verwendet, wobei die Variable [!DNL Adobe Experience Platform Mobile SDK].

In diesem Artikel wird eine iOS-Beispielanwendung mit dem [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

In der realen Welt verwendet Ihre Enterprise-App wahrscheinlich Webansichten in Ihrer mobilen App. Eine Webansicht ist ein Container, der eine Webseite mithilfe einer URL lädt. Der Container ähnelt einem Browserfenster ohne Steuerelemente. In iOS funktioniert der Webansichtsbehälter bei der Verarbeitung von Webseiten als Safari-Browser.

## Voraussetzungen 

Erste Schritte mit dem [!DNL Adobe Experience Platform Mobile SDK]müssen Sie einige vorbereitende Aufgaben ausführen.

Weitere Informationen finden Sie unter [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} Dokumentation.

## Synchronisieren von nativem Code mit Webansichten

Die Herausforderung bei der Implementierung [!DNL Target] In einer nativen App mit Webansichten lautet die Variable [!DNL Adobe Experience Platform Mobile SDK] hat bereits alle erforderlichen Kennungen generiert, die für [!DNL Adobe] -Lösungen nahtlos funktionieren. Die Identifikatoren sind jedoch noch nicht für die Webansichten sichtbar, da sie sich nicht in der nativen Plattformumgebung befinden. Daher müssen Sie eine Verbindung erstellen, um einige SDK-IDs an die Webansichten zu übergeben, damit die Besucheridentität in der Webumgebung erhalten bleibt. Andernfalls werden doppelte Besuche ausgegeben, was sich auf Ihre Berichterstellung auswirkt.

Glücklicherweise [!DNL Adobe Experience Platform Mobile SDK] bietet eine bequeme Methode zum Generieren von [!DNL Adobe] Parameter, die erforderlich sind, damit Webansichten denselben Besucher nutzen und beibehalten können, wie im folgenden Beispielcode gezeigt:

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

Weitere Informationen zum `Identity.appendTo` und ein Beispiel für die Verwendung der -Methode finden Sie unter [Swift > Beispiel](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} im *Mobile SDK-Dokumentation*.

Verwenden `Identity.appendTo`, diese URL:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

wird in:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Wie Sie sehen können, gibt es `adobe_mc` -Parameter an die URL angehängt. Dieser Parameter enthält kodierte Werte für:

* TS=1660667205: Der aktuelle Zeitstempel. Dieser Zeitstempel stellt sicher, dass die Webansicht keine abgelaufenen Werte erhält.
* MCMID=69624092487065093697422606480535692677: Die [!UICONTROL Experience Cloud-ID] (ECID). Wird auch als MID oder [!UICONTROL Marketing Cloud-ID] erforderlich für [!DNL Adobe] lösungsübergreifende Besucheridentifizierung.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: Die [!UICONTROL Adobe-Organisations-ID].

Die `Identity.getUrlVariables` ist eine Alternative [!DNL Adobe Experience Platform Mobile SDK] -Methode, die eine entsprechend geformte Zeichenfolge zurückgibt, die die [!DNL Experience Cloud Identity Service] URL-Variablen. Weitere Informationen finden Sie unter [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} im *Identity API-Referenz*.

## Übergeben Sie die [!DNL Target] Sitzungs-ID für Erlebnisse derselben Sitzung

Ein weiterer Schritt ist erforderlich, um die [!DNL Target] Benutzer-Journey funktioniert nahtlos über die nativen und Webansichten hinweg. Dieser Schritt umfasst das Extrahieren und Übergeben der [!DNL Target] Sitzungs-ID aus der [!DNL Adobe Experience Platform Mobile SDK] in die Webansichten der App.

Die `Target.getSessionId` extrahiert die Sitzungs-ID, die als `mboxSession` Parameter:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testen in Webansichten

Webvorschaulinks werden auf der Seite [!UICONTROL Aktivitätsdetails] Seite durch Klicken auf [[!UICONTROL ADOBE QA] link](/help/dev/implement/mobile/target-mobile-preview.md) , um ein Popup anzuzeigen, um jeden Erlebnisvorschau-Link zu kopieren, ähnlich dem folgenden:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Webvorschau-Links enthalten zusätzliche `at_preview_index` und `at_preview_listed_activities_only` Parameter. Kopieren Sie diese Parameter, um mobile Vorschaulinks mit Weblink-Parametern zu erstellen.

Beispiel:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Nachdem Sie den Link in einem iOS Safari-Browser geöffnet haben, erfasst Ihre App die URL in Ihrer `AppDelegate` -Klasse ähnlich dem folgenden Beispiel:

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
