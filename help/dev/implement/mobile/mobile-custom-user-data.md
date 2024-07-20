---
keywords: mobile App, Daten mit mobilen Apps senden, Targeting mobiler Apps, benutzerdefinierte Daten für Mobilnutzer, benutzerdefinierte Daten für mobile Apps
description: Erfahren Sie, wie Sie zusätzliche Informationen über den Ort oder den Benutzer als Name-Wert-Paare an [!DNL Adobe Target] senden können, um benutzerdefinierte Zielgruppen zu erstellen.
title: Wie sende ich benutzerdefinierte Benutzerdaten in einer iOS-App?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 55%

---

# iOS – Senden benutzerdefinierter Benutzerdaten

Sie können zusätzliche Informationen über den Standort oder den Benutzer als Name-Wert-Paare an [!DNL Target] senden.

>[!IMPORTANT]
>
>Unterstützung für Version 4 von [!DNL Adobe Mobile].*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr für [!DNL Adobe Target] Mobilbenutzer empfohlen.
>
>Das [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Unterstützung von [!DNL Adobe Experience Cloud] -Lösungen und -Diensten in Ihren mobilen Apps.

Mithilfe dieser Informationen können benutzerdefinierte Zielgruppen (beispielsweise Benutzer mit über 25.000 Meilen) und Berichte erstellt werden.

Es gibt zwei Parametertypen, die Sie mit einem [!DNL Target] -Aufruf senden können:

* **Mbox-Parameter**: Mbox-Parameter sind sitzungsübergreifend nicht persistent.
* **Profilparameter**: Profilparameter werden im Besucherprofilspeicher gespeichert und sind sitzungsübergreifend persistent. Mbox-Parameter bleiben nicht bestehen. Einige Schlüssel sind reserviert, es können jedoch sowohl Profil- als auch Mbox-Parameter als benutzerdefinierte Schlüsselwertpaare festgelegt werden.

Obwohl es einige reservierte Schlüssel gibt, können sowohl Profil- als auch Mbox-Parameter benutzerdefinierte Schlüsselwertpaare enthalten.

1. Erstellen Sie ein Wörterbuch.

   Erstellen Sie zunächst ein Wörterbuch mit den Werten, die Sie an [!DNL Target] übergeben möchten. Fügen Sie dieses der Einfachheit halber der Methode `welcomeMessageCampaign` hinzu, sodass Sie sich keine Gedanken über den Geltungsbereich machen müssen.

   Im Folgenden finden Sie ein Beispiel für ein Wörterbuch. Sie können dies nach `(void)welcomeMessageCampaign` kopieren. Die Werte von Schlüsseln wie `userLevel` und `userMiles` sind in diesem Beispiel hartcodiert. Allgemein können Sie die entsprechenden Variablen übermitteln.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * Schlüssel mit Präfixprofil (beispielsweise `profile.persona`) werden im Benutzerprofil gespeichert.

     Diese Profilattribute können für verschiedene Aktivitäten und Kanäle übergreifend eingesetzt werden.

   * Bei Schlüsseln ohne Präfix (beispielsweise `userMiles`) handelt es sich um Mbox-Parameter.

     Diese Parameter sind nur während der Sitzung verfügbar.

   * Schlüssel mit Präfixentität (beispielsweise `entity.category.id`) werden für Produktempfehlungen eingesetzt.

1. Prüfen Sie die Daten.
   1. Entfernen Sie in der Anwendung `didFinishLaunchingWithOptions` den Kommentar oder fügen Sie `[ADBMobile setDebugLogging:YES];` hinzu.

      Durch diese Aktion werden detaillierte Debugging-Protokolle erstellt.
   1. Erstellen Sie die Anwendung.
   1. Prüfen Sie, dass die Parameter im Target-Aufruf übermittelt werden.

      Suchen Sie in Ihrer Debugging-Konsole nach dem Namen Ihres Zielorts. Es wird ein `YOUR-CLIENT-CODE.tt.omtrdc.net` mit allen soeben übermittelten Parametern angezeigt.

      (Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

      ![Target-Speicherort in der Debug-Konsole](/help/dev/implement/mobile/assets/mobile-debug.png "Target-Speicherort in der Debug-Konsole"){zoomable="yes"}

   Sie können Zielgruppen erstellen und die Anzeige von Inhalten mithilfe dieser Parameter in [!DNL Target] einschränken oder auf sie ausrichten.
