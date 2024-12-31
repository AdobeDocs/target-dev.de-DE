---
keywords: Implementierung, API, Profil, Profil-API-Einstellungen, Authentifizierungs-Token
description: Erfahren Sie, wie Sie die Authentifizierung für Batch-Aktualisierungen über  [!DNL Adobe Target] -APIs konfigurieren und ein Profil-Authentifizierungstoken generieren.
title: Wie verwende ich Profil-API-Einstellungen, um Batch-Aktualisierungen zu aktivieren oder zu deaktivieren?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 28%

---

# Profil-API-Einstellungen

Aktivieren oder deaktivieren Sie die Authentifizierung für Batch-Aktualisierungen über [!DNL Adobe Target] APIs und generieren Sie ein Profil-Authentifizierungstoken.

[!DNL Adobe Target] erstellt und verwaltet ein Profil für jeden einzelnen Benutzer. Dieses Profil wird im [!DNL Target] Edge-Cluster gespeichert und nach jedem Besuch in Echtzeit aktualisiert. Sie können ein Profil auch einzeln oder stapelweise über die API aktualisieren.

Um die Sicherheit zu erhöhen, können Sie festlegen, dass beim API-Aufruf für die Massenaktualisierung ein gültiges Zugriffstoken in der -Kopfzeile der Anfrage übergeben werden muss.

**So erfordern Sie eine Authentifizierung und generieren ein Zugriffs-Token über die [!DNL Target] Benutzeroberfläche:**

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Wechseln Sie unter **[!UICONTROL Profile API]** Folie mit dem **[!UICONTROL Require Authentication]** in die aktivierte oder deaktivierte Position.

   ![ALT-Bild](assets/profile_api_settings.png)

1. (Bedingt) Wenn Sie die Authentifizierungspflicht aktiviert haben, klicken Sie auf **[!UICONTROL Generate New Profile Authentication Token]**.

   ![ALT-Bild](assets/profile_api_settings_2.png)

   Das Token läuft gemäß der im Feld „Läuft ab in“ angegebenen Zeit ab.

   Für die Generierung eines Authentifizierungstokens benötigen Sie eine der folgenden Benutzerberechtigungen:

   * Administratorrolle oder mindestens über Rechte als genehmigende Person verfügen

     Weitere Informationen für Target Standard-Kunden finden Sie unter [Festlegen von Rollen und Berechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) in *Benutzer*. Weitere Informationen für [!DNL Target Premium]-Kunden finden Sie unter [Konfigurieren von Enterprise-Berechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Administratorrolle auf der Ebene Arbeitsbereich/Produktprofil

     Arbeitsbereiche stehen nur [!DNL Target Premium]-Kunden zur Verfügung. Weitere Informationen finden Sie unter [Konfigurieren von Enterprise-Berechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Administratorrechte (Berechtigung „Sysadmin“) auf der [!DNL Adobe Target]-Produktebene

Sie können auch per API ein Profilauthentifizierungstoken generieren. Weitere Informationen finden Sie unter „Profile“ im [Adobe Target Admin- und Profil-API-Handbuch](../../administer/admin-api/admin-api-overview-new.md).

1. Kopieren Sie das Token und fügen Sie es in die Kopfzeile der Anfrage im Format „Autorisierung“ : „Inhaber“ ein.

1. Klicken Sie auf **[!UICONTROL Generate New Profile Authentication Token]** , um das Token nach Bedarf neu zu generieren.

>[!WARNING]
>
>Wenn Sie dieses Token zurücksetzen, schlagen API-Aufrufe mit dem aktuellen Token fehl. Dies erfordert eine Aktualisierung von Skripten oder Apps, die dieses Token verwenden.
