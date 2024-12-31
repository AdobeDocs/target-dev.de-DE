---
keywords: mobile App, SDK mobile App, Targeting mobiler Apps, mobiles Target-SDK, Target in SDK aktivieren
description: Erfahren Sie, wie Sie die Adobe Mobile Services SDK zu Ihrer Mobile App hinzufügen.
title: Wie aktiviere ich  [!DNL Target]  in der  [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 29%

---

# Aktivieren von [!DNL Target] in der SDK

Fügen Sie die [!UICONTROL Adobe Mobile Services SDK] zu Ihrer App hinzu.

>[!IMPORTANT]
>
>Unterstützung für die [!DNL Adobe Mobile] Version 4.*x* SDKs sind seit dem 31. August 2021 ausgelaufen und werden für [!DNL Adobe Target] Mobilbenutzer nicht mehr empfohlen.
>
>Die [Adobe Experience Platform SDK für Mobile Apps](https://developer.adobe.com/client-sdks/documentation/){target=_blank} ist die empfohlene Lösung für [!DNL Adobe Experience Cloud] Lösungen und Services in Ihren Mobile Apps.

1. Wenn Sie die Adobe Mobile Services SDK nicht in Ihrer App installiert haben, verwenden Sie Ihre Analytics- oder Experience Cloud-Anmeldedaten und laden Sie die SDK von der [Adobe Mobile Services](https://mobilemarketing.adobe.com/)-Website herunter.

1. Fügen Sie die [!DNL Adobe Mobile Services SDK] zu Ihrer App hinzu.

   Anweisungen hierzu finden Sie unter [Kernimplementierung und Lebenszyklus](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html).

1. Fügen Sie Kunden-Code und Zeitüberschreitung hinzu und aktivieren Sie SSL.

   Öffnen Sie auf der Experience Cloud Mobile Services und navigieren Sie zu **[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**.

   Fügen Sie Ihren [!DNL Target] Clientcode und die maximale Wartezeit hinzu. Der Kunden-Code ist ein eindeutiger Code für Ihr Konto oder Unternehmen. Die maximale Wartezeit ist die Zeit in Sekunden, bis zu der [!DNL Target] auf eine Antwort warten, bevor der Standardinhalt angezeigt wird. Stellen Sie sicher, dass die Option **[!UICONTROL Use HTTPS]** auf der Seite „Mobile-App-Einstellungen verwalten“ in Adobe Mobile Services aktiviert ist. Wenn HTTPS nicht aktiviert ist, werden alle Aufrufe in iOS9+ blockiert, es sei denn, der [!DNL Target] wird auf die Zulassungsliste gesetzt.

   ![ALT-Bild](assets/mobile-clientcode.png)

1. Nachdem Sie Ihre App erstellt/gefunden haben, suchen Sie nach den App-Einstellungen und laden Sie die gewünschte SDK herunter.

   ![ALT-Bild](assets/download-sdk.png)

>[!WARNING]
>
> Wenn Sie keinen Zugriff auf die mobile Marketing-Oberfläche haben, können Sie Änderungen direkt in der Konfigurationsdatei in Ihrem App-Code vornehmen. Dies wird jedoch nicht mit der Einstellungsseite in der Benutzeroberfläche synchronisiert.
