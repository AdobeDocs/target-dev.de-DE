---
keywords: mobile App, Ort mobiler Apps, mobile App als Ziel, Orte mobiler Apps, Erfolgsmetriken für mobile Apps
description: Sehen Sie sich den Beispiel-Code an, um zu erfahren, wie Sie Standorte und Erfolgsmetriken in iOS-Apps erstellen, damit Sie Ihre App  [!DNL Adobe Target]  und optimieren können.
title: Wie erstelle ich  [!DNL Target]  und Erfolgsmetriken in einer iOS-App?
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 66%

---

# iOS - Erstellen eines [!DNL Target] Speicherorts und einer Erfolgsmetrik

Um [!DNL Target] in Ihrer Mobile App zu verwenden, erstellen Sie einen Standort und eine Erfolgsmetrik.

>[!IMPORTANT]
>
>Unterstützung für die [!DNL Adobe Mobile] Version 4.*x* SDKs sind seit dem 31. August 2021 ausgelaufen und werden für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

In diesem Abschnitt finden Sie Beispiel-Code, der als Vorlage für Ihre App verwendet werden kann. Die Beispiele in diesem Abschnitt enthalten Code für iOS. Die gleichen Muster gelten jedoch auch für Android. Android-spezifische Syntax finden Sie im Handbuch [Android SDK 4.x for Experience Cloud Solutions](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html).

>[!NOTE]
>
>In der [Mobile-Dokumentation](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html) finden Sie eine Liste aller verfügbaren [!DNL Target].

Um einen [!DNL Target] Speicherort in Ihrer App zu erstellen und eine Anfrage zu stellen, gibt es zwei primäre Methoden:

* `targetCreateRequestWithName`
* `targetLoadRequest`

1. Erstellen Sie einen [!DNL Target].

   Hier finden Sie ein Aufrufbeispiel für die Erstellung einer Abfrage:

   ```
   // make your request 
   ADBTargetLocationRequest *myRequest = [ADBMobile targetCreateRequestWithName:@"heroBanner" 
                                                    defaultContent:@"default.png" 
                                                    parameters:nil];
   ```

   | Parameter | Beschreibung |
   |---|---|
   | `ADBTargetLocationRequest *myRequest` | Ersetzen Sie `myRequest` durch den Namen Ihrer `targetLocation` in der App. |
   | `targetCreateRequestWithName:@"heroBanner"` | Ersetzen Sie `heroBanner` durch den Namen Ihrer `targetLocation` in Target. Es handelt sich hierbei auch um den Namen der mbox. Dieses Hero-Banner wird in der Target-Oberfläche angezeigt. |
   | `defaultContent:@"default.png"` | Ersetzen Sie `default.png` durch den Wert, den die App nutzt, falls Target nicht reagiert. |
   | `parameters:nil` | Legen Sie Profil- oder Mbox-Parameter fest. Weitere Informationen finden Sie im Abschnitt über das Übermitteln benutzerdefinierter Daten. |

   Hier finden Sie ein Aufrufbeispiel für das Laden einer Abfrage:

   ```
   // load your request 
   [ADBMobile targetLoadRequest:myRequest callback:^(NSString *content) { 
                                        // do something with content 
                                        heroImage.image = [UIImage imageNamed:content]; 
   }];
   ```

   | Parameter | Beschreibung |
   |---|---|
   | `targetLoadRequest:myRequest` | Ersetzen Sie `myRequest` durch den Namen Ihrer `targetLocation` in der App. |
   | `NSString *content` | Ersetzen Sie Inhalte durch tatsächliche Inhalte, die von Adobe zurückgegeben werden. Die Zeichenfolge kann eine XML-, JSON- oder eine einfache Zeichenfolge sein. Verwenden Sie diesen Codeabschnitt für das Festlegen von Variablen, von Bildpfaden, zur Ansicht von Kontrollflüssen, Transaktionspunkten und anderen gewünschten Aktionen. Target gibt den in der UI eingegebenen Inhalt im selben Format zurück. |
   | `heroImage.image = [UIImage imageNamed:content];` | Beispiel: Nehmen Sie Inhalte und legen Sie den Pfad für ein Hero Image fest. |

1. Erstellen Sie eine Erfolgsmetrik.

   Mit der Methode `targetCreateOrderConfirmRequestWithName` können Sie Konversions-/Erfolgsmetriken in Ihrer App verfolgen.

   ```
   ADBTargetLocationRequest *req = [ADBMobile targetCreateOrderConfirmRequestWithName: "orderConfirm" 
                                              orderId: orderId 
                                              orderTotal: @"39.95" 
                                              productPurchasedId: _galleryItem.title 
                                              parameters: nil]; 
   [ADBMobile targetLoadRequest: req callback: nil];
   ```

   | Parameter | Beschreibung |
   |---|---|
   | `orderId` | Ersetzen Sie sie durch eine dynamische Variable, die für eine eindeutige Bestell-ID steht. |
   | `@"39.95"` | Ersetzen Sie sie durch eine dynamische Variable, die für eine eindeutige Bestellsumme steht. |
   | `_galleryItem.title` | Ersetzen Sie sie durch eine dynamische Variable, die für eine kommagetrennte Liste der erworbenen Produkte steht. |
   | `parameters: nil` | Optionales Wörterbuch weiterer Parameter |

1. Erstellen Sie die Anwendung.

   Führen Sie einen A/B-Test durch, nachdem Sie einen Zielort erstellt und eine Erfolgsmetrik getaggt haben. Die Aktivität kann als Form-based Experience Composer verwendet werden.
