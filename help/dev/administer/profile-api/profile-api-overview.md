---
title: Profilaktualisierung
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten an  [!DNL Target] senden.
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---

# Profilaktualisierung

Ein Benutzerprofil enthält demografische und Verhaltensinformationen eines Web-Seitenbesuchers, z. B. Alter, Geschlecht, gekaufte Produkte, letzte Besuchszeit und so weiter. [!DNL Adobe Target] verwendet diese Informationen, um den Inhalt für jeden Besucher zu personalisieren.

Die Profilinformationen für jeden Besucher werden entweder in Cookies oder in Apps von Drittanbietern gespeichert.

Wenn Ihre Web-Seite den [!DNL Target]-Code ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) oder den [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)) implementiert, werden die Profilinformationen aus den Cookies mithilfe von Profilparametern an [!DNL Target] übergeben. [!DNL Target] identifiziert jeden Besucher eindeutig anhand einer `pcID`, die in den Cookies des Besuchers generiert wird. Sie können jedoch mithilfe von `mbox3rdPartyIds` Profilparameter aus einer externen App über Mbox-Aufrufe übergeben.

Verwenden Sie die [!DNL Adobe Target]-Profil-APIs, wenn Sie Profildaten über Ihre Besucher haben, die Sie im Rahmen Ihrer seitenbasierten Integration mit [!DNL Target] an [!DNL Target] senden können, die Sie nicht senden können oder möchten. Dabei kann es sich um Daten aus einem CRM (Customer Relationship Management)- oder POS (Point of Sale)-System handeln, die auf der Seite nicht verfügbar sind. Oder diese Daten sind möglicherweise sensibler, sodass es nicht sinnvoll ist, sie auf der Seite weiterzugeben.

Es gibt zwei Möglichkeiten, Profile über die API zu aktualisieren:

* [API zur Aktualisierung von einzelnen Profilen](/help/dev/administer/profile-api/profile-single-api.md)
* [Massenaktualisierung von Profilen über Batch](/help/dev/administer/profile-api/profile-bulk-api.md)
