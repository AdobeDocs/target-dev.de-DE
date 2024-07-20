---
keywords: implementieren, implementieren, einrichten, einrichten, Seitenparameter, Tomcat, URL-kodiert, In-Page-Profilattribut, Mbox-Parameter, In-Page-Profilattribute, Skript-Profilattribute, Bulk-Profilupdate-API, Single-File-Update-API, Kundenattribute, implementieren5, implementieren6, implementieren, implementieren8, implementieren, Implementierung von0, Implementierung von2, Implementierung von4, Datenanbietern, Datenanbietern, Datenanbietern
description: Rufen Sie Daten in [!DNL Target]  ab (Seitenparameter, Profilattribute, Skript-Profilattribute, Datenanbieter, Single- und Bulk-Profil-Update-APIs, Kundenattribute).
title: Wie integriere ich Daten in Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 34%

---

# Methodenübersicht

Informationen zu den verschiedenen Methoden für die Datenübernahme in Adobe Target.

Zu den verfügbaren Methoden gehören:

| Methode | Details |
| --- | --- |
| [Seitenparameter](page-parameters.md)<br />(Auch &quot;mbox-Parameter&quot;genannt) | Seitenparameter sind Name-Wert-Paare, die direkt über den Seiten-Code übergeben und nicht zur späteren Verwendung im Profil des Besuchers gespeichert werden.<br />Seitenparameter sind nützlich, um Seitendaten an [!DNL Target] zu senden, die nicht mit dem Profil des Besuchers gespeichert werden müssen, um sie für die zukünftige Zielgruppenbestimmung verwenden zu können. Diese Werte werden stattdessen verwendet, um die Seite oder die Aktion zu beschreiben, die der Benutzer auf der jeweiligen Seite ausgeführt hat. |
| [Profilattribute auf der Seite](in-page-profile-attributes.md)<br /> (auch &quot;In-mbox-Profilattribute&quot;genannt) | Inpage-Profilattribute sind Name-Wert-Paare, die direkt über den Seiten-Code übergeben werden und im Profil des Besuchers für die zukünftige Verwendung gespeichert werden.<br />In-page-Profilattribute ermöglichen die Speicherung benutzerspezifischer Daten im Target-Profil zum späteren Targeting und zur späteren Segmentierung. |
| [Skriptprofilattribute](script-profile-attributes.md) | Skript-Profilattribute sind Name/Wert-Paare, die in der [!DNL Target] -Lösung definiert sind. Der Wert wird durch die Ausführung eines JavaScript-Snippets auf dem Target-Server über den Server-Aufruf ermittelt.<br />Benutzer schreiben kleine Code-Snippets, die pro Mbox-Aufruf ausgeführt werden und bevor ein Besucher auf die Zielgruppe und Aktivitätsmitgliedschaft ausgewertet wird. |
| [Datenanbieter](data-providers.md) | Mit Datenanbietern können Sie Daten von Drittanbietern einfach an Target weitergeben. |
| [API zur Bulk-Aktualisierung von Profilen](bulk-profile-update-api.md) | Senden Sie über die API eine CSV-Datei an [!DNL Target] mit aktualisierten Besucherprofilen für viele Besucher. Jedes Besucherprofil kann mit mehreren In-Page-Profilattributen in einem Aufruf aktualisiert werden. |
| [API zur Aktualisierung von einzelnen Profilen](single-profile-update-api.md) | Fast identisch mit der Bulk Profile Update API, aber ein Besucherprofil wird gleichzeitig aktualisiert, und zwar in Übereinstimmung mit dem API-Aufruf und nicht mit einer CSV-Datei. |
| [Kundenattribute](customer-attributes.md) | Mithilfe von Kundenattributen können Sie Besucherprofildaten per FTP in die Experience Cloud hochladen. Verwenden Sie nach dem Hochladen die Daten in Adobe Analytics und Adobe Target. |
