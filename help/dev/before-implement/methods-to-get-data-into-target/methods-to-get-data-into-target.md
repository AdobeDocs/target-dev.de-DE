---
keywords: Implementieren, Implementieren, Einrichten, Einrichtung, Seitenparameter, Tomcat, URL-kodiert, In-Page-Profilattribut, Mbox-Parameter, In-Page-Profilattribute, Skript-Profilattribut, Bulk Profile Update API, Single File Update API, Kundenattribute, Implementieren5, Implementieren6, Implementieren7, Implementieren8, Implementieren9, Implementieren0, Implementieren1, Implementieren2, Implementieren3, Implementieren4, Implementieren5, Datenanbieter, Datenanbieter, Datenanbieter
description: Daten in abrufen  [!DNL Target] Seitenparameter, Profilattribute, Skriptprofilattribute, Datenanbieter, APIs zur Aktualisierung von Einzel- und Massenprofilen, Kundenattribute).
title: Wie integriere ich Daten in Target?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
TQID: https://experienceleague.adobe.com/pmlPWRHb9tnrdSFm7s5OZ-RRsJJOxw-ntBY5AeswIcM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 27%

---

# Methodenübersicht

Informationen zu den verschiedenen Methoden, mit denen Sie Daten in Adobe Target importieren können.

Zu den verfügbaren Methoden gehören:

| Methode | Details |
| --- | --- |
| [Seitenparameter](page-parameters.md)<br />(auch als „mbox-Parameter“ bezeichnet) | Seitenparameter sind Name-Wert-Paare, die direkt über den Seiten-Code übergeben und nicht zur späteren Verwendung im Profil des Besuchers gespeichert werden.<br />Seitenparameter sind nützlich, um Seitendaten an [!DNL Target] zu senden, die nicht im Besucherprofil gespeichert werden müssen, damit sie in Zukunft für das Targeting verwendet werden können. Diese Werte werden stattdessen verwendet, um die Seite oder die Aktion zu beschreiben, die der Benutzer auf der jeweiligen Seite ausgeführt hat. |
| [In-Page-Profilattribute](in-page-profile-attributes.md)<br /> (auch „In-Mbox-Profilattribute“ genannt) | Seiteninterne Profilattribute sind Name/Wert-Paare, die direkt durch den Seiten-Code übergeben werden und im Besucherprofil für die zukünftige Verwendung gespeichert werden. <br />Seiteninterne Profilattribute ermöglichen die Speicherung benutzerspezifischer Daten im Target-Profil für späteres Targeting und Segmentierung. |
| [Skriptprofilattribute](script-profile-attributes.md) | Skriptprofilattribute sind Name/Wert-Paare, die in der [!DNL Target]-Lösung definiert sind. Der Wert wird durch die Ausführung eines JavaScript-Snippets auf dem Target-Server über den Server-Aufruf ermittelt.<br />Benutzer schreiben kleine Code-Snippets, die pro Mbox-Aufruf und vor der Prüfung eines Besuchers auf Zielgruppen- und Aktivitätsmitgliedschaft ausgeführt werden. |
| [Datenanbieter](data-providers.md) | Mit Datenanbietern können Sie mühelos Daten von Drittanbietern an Target weitergeben. |
| [API zur Bulk-Aktualisierung von Profilen](bulk-profile-update-api.md) | Senden Sie über die -API für viele Besucher eine CSV-Datei an [!DNL Target] mit Aktualisierungen des Besucherprofils. Jedes Besucherprofil kann mit mehreren In-Page-Profilattributen in einem Aufruf aktualisiert werden. |
| [API zur Aktualisierung von einzelnen Profilen](single-profile-update-api.md) | Beinahe identisch mit der API zur Massenaktualisierung von Profilen, wird jedoch jeweils ein Besucherprofil aktualisiert, und zwar in Zeile mit dem API-Aufruf anstelle einer CSV-Datei. |
| [Kundenattribute](customer-attributes.md) | Mithilfe von Kundenattributen können Sie Besucherprofildaten per FTP in die Experience Cloud hochladen. Verwenden Sie die Daten nach dem Hochladen in Adobe Analytics und Adobe Target. |
