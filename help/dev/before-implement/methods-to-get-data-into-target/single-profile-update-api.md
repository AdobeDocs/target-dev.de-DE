---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Einzelprofil-Update
description: Daten abrufen [!DNL Target] Verwendung der API für die Aktualisierung einzelner Profile.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der Single-Profile-Update-API?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 13%

---

# Single Profile Update API

Fast identisch mit dem [!UICONTROL Bulk-Profil-Update-API] in [!DNL Adobe Target], jedoch wird jeweils ein Besucherprofil aktualisiert, und zwar in Übereinstimmung mit dem API-Aufruf anstelle der CSV-Datei.

## Format

Der Besucher muss über die Variable [!DNL Target] `mboxPC` Wert oder `mbox3rdPartyId` -Wert. Die [!UICONTROL Experience Cloud-ID] (ECID) wird nicht unterstützt.

## Anwendungsbeispiele

Sie möchten das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Zu den Aktionen gehören das Erreichen eines Callcenters, die Finanzierung eines Darlehens, die Verwendung einer Treuekarte im Geschäft, der Zugriff auf einen Kiosk usw.

## Vorteile der Methode

* Keine Begrenzung der Anzahl der Profilattribute.*
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen 

* Begrenzung auf 1.000.000 (1 Million) API-Aufrufe pro 24-Stunden-Zeitraum.
* Aktualisiert nur Profile. Profil kann nicht für einen potenziellen Benutzer erstellt werden [!DNL Target] hat noch nicht gesehen.
* Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.

## Codebeispiele

GET und POST werden unterstützt. 

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Ressourcen

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
