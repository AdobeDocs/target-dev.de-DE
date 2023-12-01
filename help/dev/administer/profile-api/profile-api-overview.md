---
title: Übersicht über Adobe Target Profile-APIs
description: Erfahren Sie, wie Sie mit Adobe Target Profile-APIs Besucherdaten an senden können. [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# [!DNL Adobe Target Profile APIs overview]

Ein Benutzerprofil enthält demografische und verhaltensbezogene Informationen eines Webseitenbesuchers, z. B. Alter, Geschlecht, gekaufte Produkte, letzter Besuch usw. [!DNL Adobe Target] verwendet diese Informationen, um den Inhalt zu personalisieren, der jedem Besucher bereitgestellt wird.

Die Profilinformationen für jeden Besucher werden entweder in Cookies oder in Drittanbieter-Apps gespeichert.

Wenn Ihre Webseite den Target-Code implementiert ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) oder [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)), werden die Profilinformationen aus den Cookies an [!DNL Target] unter Verwendung von Profilparametern. [!DNL Target] identifiziert jeden Besucher eindeutig über eine `pcID` dass sie die Cookies des Besuchers generiert. Sie können Profilparameter jedoch von einer externen App über Mbox-Aufrufe mit `mbox3rdPartyIds`.

Verwenden Sie die [!DNL Adobe Target] Profil-APIs, wenn Sie Profildaten zu Ihren Besuchern haben, die an gesendet werden sollen [!DNL Target] , die Sie im Rahmen Ihrer seitenbasierten Integration mit [!DNL Target]. Dies können Daten aus einem CRM-System (Customer Relationship Management) oder POS-System (Point of Sale) sein, die nicht auf der Seite verfügbar sind, oder Daten sensiblerer Art, die nicht sinnvoll sind, um die Seite weiterzugeben.

Es gibt zwei Möglichkeiten, Profile über API zu aktualisieren:

* [API zur Aktualisierung von einzelnen Profilen](/help/dev/administer/profile-api/profile-single-api.md)
* [Massenprofilaktualisierung über Batch](/help/dev/administer/profile-api/profile-bulk-api.md)
