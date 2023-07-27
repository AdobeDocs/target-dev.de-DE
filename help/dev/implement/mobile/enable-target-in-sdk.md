---
keywords: mobile App, SDK mobile App, Targeting mobiler Apps, mobiles Target-SDK, Target in SDK aktivieren
description: Erfahren Sie, wie Sie die Adobe Mobile Services SDK zu Ihrer App hinzufügen.
title: Wie aktiviere ich [!DNL Target] im [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 49%

---

# Aktivieren [!DNL Target] im SDK

Fügen Sie die [!UICONTROL Adobe Mobile Services SDK] auf Ihre App.

>[!IMPORTANT]
>
>Unterstützung für [!DNL Adobe Mobile] Version 4.*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr empfohlen für [!DNL Adobe Target] Mobilbenutzer.
>
>Die [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Stromversorgung [!DNL Adobe Experience Cloud] Lösungen und Dienste in Ihren mobilen Apps.

1. Wenn Sie das Adobe Mobile Services SDK nicht in Ihrer App installiert haben, verwenden Sie Ihre Analytics- oder Experience Cloud-Anmeldeinformationen und laden Sie das SDK von der [Adobe Mobile Services](https://mobilemarketing.adobe.com/)-Website herunter.

1. Fügen Sie die [!DNL Adobe Mobile Services SDK] auf Ihre App.

   Anweisungen hierzu finden Sie unter [Kernimplementierung und Lebenszyklus](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Fügen Sie Kunden-Code und Zeitüberschreitung hinzu und aktivieren Sie SSL.

   Öffnen Sie „Mobile Services“ in der Experience Cloud und navigieren Sie zu **[!UICONTROL App-Einstellungen verwalten]** > **[!UICONTROL SDK-Target-Optionen]**.

   Fügen Sie Ihre [!DNL Target] Clientcode und Zeitüberschreitung. Der Kunden-Code ist ein eindeutiger Code für Ihr Konto oder Unternehmen. Die Zeitüberschreitung ist die Zeit in Sekunden, bis zu der [!DNL Target] wartet auf eine Antwort, bevor der Standardinhalt angezeigt wird. Stellen Sie sicher, dass Sie die Option **[!UICONTROL HTTPS verwenden]** auf der Seite „App-Einstellungen verwalten“ in Adobe Mobile Services aktiviert haben. Wenn HTTPS nicht aktiviert ist, werden alle Aufrufe in iOS9+ blockiert, es sei denn, Sie haben die Option [!DNL Target] Server.

   ![ALT-Bild](assets/mobile-clientcode.png)

1. Nachdem Sie Ihre App erstellt/gefunden haben, suchen Sie die App-Einstellungen und laden Sie das gewünschte SDK herunter.

   ![ALT-Bild](assets/download-sdk.png)

>[!WARNING]
>
> Wenn Sie keinen Zugriff auf die mobile Marketing-Oberfläche haben, können Sie Änderungen direkt in der Konfigurationsdatei in Ihrem App-Code vornehmen. Dies wird jedoch nicht mit der Einstellungsseite in der Benutzeroberfläche synchronisiert.
