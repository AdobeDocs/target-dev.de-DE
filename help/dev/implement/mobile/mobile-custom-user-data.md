---
keywords: mobile App, Daten mit mobilen Apps senden, Targeting mobiler Apps, benutzerdefinierte Daten für Mobilnutzer, benutzerdefinierte Daten für mobile Apps
description: Erfahren Sie, wie Sie zusätzliche Informationen über den Speicherort oder den Benutzer senden, um sie als Name-Wert-Paare zu [!DNL Adobe Target] und so benutzerdefinierte Zielgruppen zu erstellen.
title: Wie sende ich benutzerdefinierte Benutzerdaten in einer iOS-App?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 55%
---
# iOS – Senden benutzerdefinierter Benutzerdaten

Sie können zusätzliche Informationen über den Speicherort oder den Benutzer senden, die als Name-Wert-Paare [!DNL Target] werden sollen.

>[!IMPORTANT]
>
>Die Unterstützung für die [!DNL Adobe Mobile] Version 4.*x*-SDKs endete am 31. August 2021 und wird für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

Mithilfe dieser Informationen können benutzerdefinierte Zielgruppen (beispielsweise Benutzer mit über 25.000 Meilen) und Berichte erstellt werden.

Es gibt zwei Arten von Parametern, die Sie mit einem [!DNL Target]-Aufruf senden können:

* **Mbox-Parameter**: Mbox-Parameter sind sitzungsübergreifend nicht persistent.
* **Profilparameter**: Profilparameter werden im Profilspeicher des Besuchers gespeichert und sind sitzungsübergreifend persistent. Mbox-Parameter bleiben nicht erhalten. Einige Schlüssel sind reserviert, es können jedoch sowohl Profil- als auch Mbox-Parameter als benutzerdefinierte Schlüsselwertpaare festgelegt werden.

Obwohl es einige reservierte Schlüssel gibt, können sowohl Profil- als auch Mbox-Parameter benutzerdefinierte Schlüsselwertpaare enthalten.

1. Erstellen Sie ein Wörterbuch.

   Erstellen Sie zunächst ein Wörterbuch mit den Werten, die Sie an [!DNL Target] senden. Fügen Sie dieses der Einfachheit halber der Methode `welcomeMessageCampaign` hinzu, sodass Sie sich keine Gedanken über den Geltungsbereich machen müssen.

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

      (Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

      ![Zielspeicherort in der Debugkonsole](/help/dev/implement/mobile/assets/mobile-debug.png "Zielspeicherort in der Debugkonsole"){zoomable="yes"}

   Mit diesen Parametern können Sie Zielgruppen erstellen und die Anzeige von Inhalten in [!DNL Target] einschränken oder auf bestimmte Zielgruppen ausrichten.
