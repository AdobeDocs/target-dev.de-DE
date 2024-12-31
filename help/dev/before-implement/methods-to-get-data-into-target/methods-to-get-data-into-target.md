---
keywords: Implementieren, Implementieren, Einrichten, Einrichtung, Seitenparameter, Tomcat, URL-kodiert, In-Page-Profilattribut, Mbox-Parameter, In-Page-Profilattribute, Skript-Profilattribut, Bulk Profile Update API, Single File Update API, Kundenattribute, Implementieren5, Implementieren6, Implementieren7, Implementieren8, Implementieren9, Implementieren0, Implementieren1, Implementieren2, Implementieren3, Implementieren4, Implementieren5, Datenanbieter, Datenanbieter, Datenanbieter
description: Daten in abrufen  [!DNL Target] Seitenparameter, Profilattribute, Skriptprofilattribute, Datenanbieter, APIs zur Aktualisierung von Einzel- und Massenprofilen, Kundenattribute).
title: Wie integriere ich Daten in Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 34%

---

# Methodenübersicht

Informationen zu den verschiedenen Methoden, mit denen Sie Daten in Adobe Target importieren können.

Zu den verfügbaren Methoden gehören:

| Methode | Details |
| --- | --- |
| [Seitenparameter](page-parameters.md)<br />(auch als „mbox-Parameter“ bezeichnet) | Seitenparameter sind Name-Wert-Paare, die direkt über den Seiten-Code übergeben und nicht zur späteren Verwendung im Profil des Besuchers gespeichert werden.<br />Seitenparameter sind nützlich, um Seitendaten an [!DNL Target] zu senden, die nicht im Besucherprofil gespeichert werden müssen, damit sie in Zukunft für das Targeting verwendet werden können. Diese Werte werden stattdessen verwendet, um die Seite oder die Aktion zu beschreiben, die der Benutzer auf der jeweiligen Seite ausgeführt hat. |
| [In-Page-Profilattribute](in-page-profile-attributes.md)<br /> (auch „In-Mbox-Profilattribute“ genannt) | Inpage-Profilattribute sind Name-Wert-Paare, die direkt über den Seiten-Code übergeben werden und im Profil des Besuchers für die zukünftige Verwendung gespeichert werden.<br />In-Page-Profilattribute ermöglichen es, benutzerspezifische Daten im Zielgruppenprofil für späteres Targeting und die Segmentierung zu speichern. |
| [Skriptprofilattribute](script-profile-attributes.md) | Skriptprofilattribute sind Name/Wert-Paare, die in der [!DNL Target]-Lösung definiert sind. Der Wert wird durch die Ausführung eines JavaScript-Snippets auf dem Target-Server über den Server-Aufruf ermittelt.<br />Benutzer schreiben kleine Code-Snippets, die pro Mbox-Aufruf und vor der Prüfung eines Besuchers auf Zielgruppen- und Aktivitätsmitgliedschaft ausgeführt werden. |
| [Datenanbieter](data-providers.md) | Mit Datenanbietern können Sie mühelos Daten von Drittanbietern an Target weitergeben. |
| [API zur Bulk-Aktualisierung von Profilen](bulk-profile-update-api.md) | Senden Sie über die -API für viele Besucher eine CSV-Datei an [!DNL Target] mit Aktualisierungen des Besucherprofils. Jedes Besucherprofil kann mit mehreren In-Page-Profilattributen in einem Aufruf aktualisiert werden. |
| [API zur Aktualisierung von einzelnen Profilen](single-profile-update-api.md) | Beinahe identisch mit der API zur Massenaktualisierung von Profilen, wird jedoch jeweils ein Besucherprofil aktualisiert, und zwar in Zeile mit dem API-Aufruf anstelle einer CSV-Datei. |
| [Kundenattribute](customer-attributes.md) | Mithilfe von Kundenattributen können Sie Besucherprofildaten per FTP in die Experience Cloud hochladen. Verwenden Sie die Daten nach dem Hochladen in Adobe Analytics und Adobe Target. |
