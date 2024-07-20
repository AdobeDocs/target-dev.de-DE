---
keywords: mobile App, SDK mobile App, Targeting mobiler Apps, mobiles Target-SDK, Target in SDK aktivieren
description: Erfahren Sie, wie Sie das Adobe Mobile Services SDK zu Ihrer Mobile App hinzufügen.
title: Wie aktiviere ich [!DNL Target] im  [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 29%

---

# Aktivieren Sie [!DNL Target] im SDK

Fügen Sie Ihrer App die [!UICONTROL Adobe Mobile Services SDK] hinzu.

>[!IMPORTANT]
>
>Unterstützung für Version 4 von [!DNL Adobe Mobile].*x* SDKs sind seit dem 31. August 2021 beendet und werden nicht mehr für [!DNL Adobe Target] Mobilbenutzer empfohlen.
>
>Das [Adobe Experience Platform SDK für mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für die Unterstützung von [!DNL Adobe Experience Cloud] -Lösungen und -Diensten in Ihren mobilen Apps.

1. Wenn Sie das Adobe Mobile Services SDK nicht in Ihrer App installiert haben, verwenden Sie Ihre Analytics- oder Experience Cloud-Anmeldeinformationen und laden Sie das SDK von der Website [Adobe Mobile Services](https://mobilemarketing.adobe.com/) herunter.

1. Fügen Sie Ihrer App die [!DNL Adobe Mobile Services SDK] hinzu.

   Anweisungen hierzu finden Sie unter [Kernimplementierung und Lebenszyklus](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Fügen Sie Kunden-Code und Zeitüberschreitung hinzu und aktivieren Sie SSL.

   Öffnen Sie auf der Experience Cloud Mobile Services und gehen Sie dann zu **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Fügen Sie Ihren [!DNL Target] Clientcode und die Zeitüberschreitung hinzu. Der Kunden-Code ist ein eindeutiger Code für Ihr Konto oder Unternehmen. Die Zeitüberschreitung ist die Zeit in Sekunden, bis [!DNL Target] auf eine Antwort wartet, bevor der Standardinhalt angezeigt wird. Stellen Sie sicher, dass die Option **[!UICONTROL Use HTTPS]** auf der Seite &quot;App-Einstellungen verwalten&quot;in Adobe Mobile Services aktiviert ist. Wenn HTTPS nicht aktiviert ist, werden alle Aufrufe in iOS9+ blockiert, es sei denn, Sie haben den [!DNL Target] -Server auf die Zulassungsliste gesetzt.

   ![alt image](assets/mobile-clientcode.png)

1. Nachdem Sie Ihre App erstellt/gefunden haben, suchen Sie die App-Einstellungen und laden Sie das gewünschte SDK herunter.

   ![alt image](assets/download-sdk.png)

>[!WARNING]
>
> Wenn Sie keinen Zugriff auf die mobile Marketing-Oberfläche haben, können Sie Änderungen direkt in der Konfigurationsdatei in Ihrem App-Code vornehmen. Dies wird jedoch nicht mit der Einstellungsseite in der Benutzeroberfläche synchronisiert.
