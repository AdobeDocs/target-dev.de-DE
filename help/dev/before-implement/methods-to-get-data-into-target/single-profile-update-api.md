---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Einzelprofil-Update
description: Daten abrufen [!DNL Target] Verwendung der API für die Aktualisierung einzelner Profile.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden der Single-Profile-Update-API?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 3ae2391dea9994c0ddc1df39d74cccf6e067c1a4
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 30%

---

# API zur Aktualisierung von einzelnen Profilen

Fast identisch mit dem [!UICONTROL Bulk-Profil-Update-API] in [!DNL Adobe Target], jedoch wird jeweils ein Besucherprofil aktualisiert, und zwar in Übereinstimmung mit dem API-Aufruf anstelle der CSV-Datei.

## Format

Der Besucher muss über die Variable [!DNL Target] mboxPC-Wert oder `mbox3rdPartyId` -Wert. Die Experience Cloud ID (ECID) wird nicht unterstützt.

## Beispielhafte Anwendungsfälle

Sie möchten das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Zu den Aktionen gehören das Erreichen eines Callcenters, die Finanzierung eines Darlehens, die Verwendung einer Treuekarte im Geschäft, der Zugriff auf einen Kiosk usw.

## Vorteile der Methode

Keine Begrenzung der Anzahl der Profilattribute.

Profilattribute, die über die Website gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen

Begrenzung auf 1.000.000 (1 Million) API-Aufrufe pro 24-Stunden-Zeitraum

Aktualisiert nur Profile. Profil kann nicht für einen potenziellen Benutzer erstellt werden [!DNL Target] hat noch nicht gesehen.

Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.

## Codebeispiele

GET und POST werden unterstützt. 

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## Ressourcen

* [Update von Profilen](https://developers.adobetarget.com/api/#updating-profiles)
