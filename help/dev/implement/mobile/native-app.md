---
keywords: Mobile App,AEP-SDK,native App,Web-Ansichten,nativ;SWIFT,Adobe Experience Platform Mobile SDK,Mobile SDK,nativer Code
description: Erfahren Sie, wie Sie  [!DNL Adobe Target]  mit  [!DNL AEP Mobile SDK]  in einer nativen App mit Web-Ansichten implementieren.
title: Implementieren  [!DNL Adobe Target]  in einer Mobile App, die nativen Code mit Web-Ansichten verwendet
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Implementieren von [!DNL Target] mit dem [!DNL AEP Mobile SDK] in einer nativen App mit Web-Ansichten

In diesem Artikel werden Best Practices für die Implementierung von [!DNL Adobe Target] in einer Mobile App vorgestellt, die nativen Code mit Web-Ansichten verwendet, die den -[!DNL Adobe Experience Platform Mobile SDK] verwenden.

In diesem Artikel werden eine Beispiel-App für iOS mit dem [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} und eine [!DNL Target] Integration verwendet, die in [Swift aus dem GitHub-Repository geschrieben wurde](https://github.com/adobe/aep-sdk-app/){target=_blank}.

In der realen Welt verwendet Ihre Unternehmens-App wahrscheinlich Web-Ansichten in Ihrer Mobile App. Eine Webansicht ist ein Container, der eine Webseite mithilfe einer URL lädt. Der Container ähnelt einem Browserfenster ohne Steuerelemente. In iOS funktioniert der Webansichts-Container als Safari-Browser bei der Verarbeitung von Web-Seiten.

## Voraussetzungen 

Um mit dem [!DNL Adobe Experience Platform Mobile SDK] zu beginnen, müssen Sie einige erforderliche Aufgaben ausführen.

Weitere Informationen finden Sie unter [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in der [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}.

## Synchronisieren von nativem Code mit Web-Ansichten

Die Herausforderung bei der Implementierung von [!DNL Target] in einer nativen App mit Web-Ansichten besteht darin, dass der [!DNL Adobe Experience Platform Mobile SDK] bereits alle erforderlichen Kennungen generiert hat, damit [!DNL Adobe] Lösungen nahtlos funktionieren. Die Identifikatoren sind jedoch noch nicht für die Web-Ansichten sichtbar, da sich diese Identifikatoren nicht in der nativen Platform-Umgebung befinden. Daher müssen Sie eine Brücke erstellen, um einige SDK-Kennungen an die Web-Ansichten zu übergeben, damit die Besucheridentität in der Web-Umgebung erhalten bleibt. Wird dies nicht ordnungsgemäß durchgeführt, kommt es zu doppelten Besuchen, was sich auf Ihre Berichte auswirkt.

Glücklicherweise bietet die [!DNL Adobe Experience Platform Mobile SDK] eine praktische Methode zum Generieren [!DNL Adobe] Parameter, die erforderlich sind, damit Web-Ansichten für denselben Besucher nutzen und beibehalten werden, wie im folgenden Beispiel-Code gezeigt:

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

Weitere Informationen zur `Identity.appendTo` und ein Beispiel für die Verwendung der Methode finden Sie unter [Swift > Beispiel](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} in der *Dokumentation zu Mobile SDK*.

Diese URL verwendet `Identity.appendTo`:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

Transformiert in:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

Wie Sie sehen können, ist an die URL `adobe_mc` Parameter angehängt. Dieser Parameter enthält kodierte Werte für:

* TS=1660667205: Der aktuelle Zeitstempel. Dieser Zeitstempel stellt sicher, dass die Web-Ansicht keine abgelaufenen Werte erhält.
* MCMID=69624092487065093697422606480535692677: Die [!UICONTROL Experience Cloud ID] (ECID). Wird auch als MID oder [!UICONTROL Marketing Cloud ID] bezeichnet, die für [!DNL Adobe] lösungsübergreifende Besucheridentifizierung erforderlich sind.
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg: Die [!UICONTROL Adobe Organization ID].

Die `Identity.getUrlVariables` ist eine alternative [!DNL Adobe Experience Platform Mobile SDK]-Methode, die eine entsprechend geformte Zeichenfolge zurückgibt, die die [!DNL Experience Cloud Identity Service] URL-Variablen enthält. Weitere Informationen finden Sie unter [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} in der *Identity API-Referenz*.

## Übergeben Sie die [!DNL Target] Sitzungs-ID für das Erlebnis in derselben Sitzung

Ein zusätzlicher Schritt ist erforderlich, damit die [!DNL Target]-Benutzer-Journey nahtlos über die native und die Web-Ansicht hinweg funktioniert. Dieser Schritt umfasst das Extrahieren und Übergeben der [!DNL Target] Sitzungs-ID aus dem [!DNL Adobe Experience Platform Mobile SDK] an die Web-Ansichten der Mobile App.

Der `Target.getSessionId` extrahiert die Sitzungs-ID, die als `mboxSession` Parameter an die Web-Ansicht-URL übergeben werden kann:

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## Testen in den Web-Ansichten

Webvorschau-Links werden auf der Seite [!UICONTROL Activity detail] generiert, indem Sie auf den Link [[!UICONTROL Adobe QA] klicken](/help/dev/implement/mobile/target-mobile-preview.md) um ein Popup zum Kopieren jedes Erlebnisvorschau-Links anzuzeigen, ähnlich dem folgenden:

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Webvorschau-Links enthalten zusätzliche `at_preview_index` und `at_preview_listed_activities_only`. Kopieren Sie diese Parameter, um für Mobilgeräte freundliche Vorschau-Links mit Weblink-Parametern zu erstellen.

Beispiel:

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Nach dem Öffnen des Links in einem iOS Safari-Browser erfasst Ihre App die URL in Ihrer `AppDelegate` ähnlich dem folgenden Beispiel:

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

Nachdem Sie nun alle erforderlichen Parameter in der App erfasst haben, können Sie sie bei Bedarf an das Web übergeben:

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

Die endgültige Ausgabe für den Web-Ansichtslink könnte wie folgt aussehen:

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
