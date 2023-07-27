---
keywords: Implementierung, API, Profil, Profil-API-Einstellungen, Authentifizierungs-Token
description: Erfahren Sie, wie Sie die Authentifizierung für Batch-Aktualisierungen konfigurieren [!DNL Adobe Target] APIs erstellen und ein Profilauthentifizierungstoken generieren.
title: Wie kann ich mithilfe der Profil-API-Einstellungen Batch-Aktualisierungen aktivieren oder deaktivieren?
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 39%

---

# Profil-API-Einstellungen

Aktivieren oder deaktivieren Sie die Authentifizierung für Batch-Aktualisierungen über [!DNL Adobe Target] APIs erstellen und ein Profilauthentifizierungstoken generieren.

[!DNL Adobe Target] erstellt und pflegt ein Profil für jeden individuellen Benutzer. Dieses Profil wird im [!DNL Target] Edge-Cluster und wird in Echtzeit nach jedem Besuch aktualisiert. Sie können ein Profil auch einzeln oder stapelweise über die API aktualisieren.

Für noch mehr Sicherheit können Sie festlegen, dass beim API-Aufruf für die Massenaktualisierung ein gültiges Zugriffstoken im Header der Anforderung übergeben werden muss.

**So fordern Sie eine Authentifizierung an und generieren ein Zugriffstoken mithilfe der [!DNL Target] Benutzeroberfläche:**

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.
1. under **[!UICONTROL Profil-API]** Folie **[!UICONTROL Authentifizierung erforderlich]** Wechsel zur aktivierten oder deaktivierten Position.

   ![ALT-Bild](assets/profile_api_settings.png)

1. (Bedingt) Wenn Sie die Authentifizierungspflicht aktiviert haben, klicken Sie auf **[!UICONTROL Neues Profilauthentifizierungstoken generieren]**.

   ![ALT-Bild](assets/profile_api_settings_2.png)

   Das Token läuft gemäß der Angabe im Feld Läuft ab in ab.

   Für die Generierung eines Authentifizierungstokens benötigen Sie eine der folgenden Benutzerberechtigungen:

   * Administratorrolle oder mindestens Genehmigerrechte haben

     Weitere Informationen für Target Standard-Kunden finden Sie unter [Rollen und Berechtigungen festlegen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) in *Benutzer*. Weitere Informationen für [!DNL Target Premium]-Kunden finden Sie unter [Konfigurieren von Enterprise-Berechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Administratorrolle auf der Ebene Arbeitsbereich/Produktprofil

     Arbeitsbereiche stehen nur [!DNL Target Premium]-Kunden zur Verfügung. Weitere Informationen finden Sie unter [Konfigurieren von Enterprise-Berechtigungen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

   * Administratorrechte (Berechtigung „Sysadmin“) auf der [!DNL Adobe Target]-Produktebene

Sie können auch per API ein Profilauthentifizierungstoken generieren. Weitere Informationen finden Sie unter &quot;Profile&quot;im [Handbuch zur Adobe Target Admin- und Profil-API](../../administer/admin-api/admin-api-overview-new.md).

1. Kopieren Sie das Token und fügen Sie es in die Kopfzeile der Anfrage im folgenden Format ein: &quot;Autorisierung&quot;: &quot;Träger&quot;.

1. Klicks **[!UICONTROL Neues Profilauthentifizierungstoken generieren]** , um das Token nach Bedarf neu zu generieren.

>[!WARNING]
>
>Wenn Sie dieses Token zurücksetzen, schlagen API-Aufrufe mit dem aktuellen Token fehl. Dies erfordert eine Aktualisierung von Skripten oder Apps, die dieses Token verwenden.
