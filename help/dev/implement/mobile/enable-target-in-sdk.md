---
keywords: mobile App, SDK mobile App, Targeting mobiler Apps, mobiles Target-SDK, Target in SDK aktivieren
description: Erfahren Sie, wie Sie die Adobe Mobile Services-SDK zu Ihrer Mobile App hinzufügen.
title: Wie aktiviere ich [!DNL Target] im [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
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
source-wordcount: '303'
ht-degree: 38%
---
# Aktivieren von [!DNL Target] in der SDK

Fügen Sie die [!UICONTROL Adobe Mobile Services SDK] zu Ihrer App hinzu.

>[!IMPORTANT]
>
>Die Unterstützung für die [!DNL Adobe Mobile] Version 4.*x*-SDKs endete am 31. August 2021 und wird für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

1. Wenn Sie Adobe Mobile Services SDK nicht in Ihrer App installiert haben, verwenden Sie Ihre Analytics- oder Experience Cloud-Anmeldedaten und laden Sie die SDK von der [Adobe Mobile Services](https://mobilemarketing.adobe.com/)-Website herunter.

1. Fügen Sie die [!DNL Adobe Mobile Services SDK] zu Ihrer App hinzu.

   Anweisungen hierzu finden Sie unter [Kernimplementierung und Lebenszyklus](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Fügen Sie Kunden-Code und Zeitüberschreitung hinzu und aktivieren Sie SSL.

   Öffnen Sie „Mobile Services“ in der Experience Cloud und navigieren Sie zu **[!UICONTROL App-Einstellungen verwalten]** > **[!UICONTROL SDK-Target-Optionen]**.

   Fügen Sie Ihren [!DNL Target] Clientcode und die maximale Wartezeit hinzu. Der Kunden-Code ist ein eindeutiger Code für Ihr Konto oder Unternehmen. Die maximale Wartezeit ist die Zeit in Sekunden, bis zu der [!DNL Target] auf eine Antwort warten, bevor der Standardinhalt angezeigt wird. Stellen Sie sicher, dass Sie die Option **[!UICONTROL HTTPS verwenden]** auf der Seite „App-Einstellungen verwalten“ in Adobe Mobile Services aktiviert haben. Wenn HTTPS nicht aktiviert ist, werden alle Aufrufe in iOS9+ blockiert, es sei denn, der [!DNL Target] wird auf die Zulassungsliste gesetzt.

   ![ALT-Bild](assets/mobile-clientcode.png)

1. Nachdem Sie Ihre App erstellt/gefunden haben, suchen Sie nach den App-Einstellungen und laden Sie die gewünschte SDK herunter.

   ![ALT-Bild](assets/download-sdk.png)

>[!WARNING]
>
> Wenn Sie keinen Zugriff auf die mobile Marketing-Oberfläche haben, können Sie Änderungen direkt in der Konfigurationsdatei in Ihrem App-Code vornehmen. Dies wird jedoch nicht mit der Einstellungsseite in der Benutzeroberfläche synchronisiert.
