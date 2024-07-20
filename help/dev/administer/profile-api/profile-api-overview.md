---
title: Profilaktualisierung
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten an  [!DNL Target] senden können.
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---

# Profilaktualisierung

Ein Benutzerprofil enthält demografische und verhaltensbezogene Informationen eines Webseitenbesuchers, z. B. Alter, Geschlecht, gekaufte Produkte, letzter Besuch usw. [!DNL Adobe Target] verwendet diese Informationen, um den Inhalt zu personalisieren, der jedem Besucher bereitgestellt wird.

Die Profilinformationen für jeden Besucher werden entweder in Cookies oder in Drittanbieter-Apps gespeichert.

Wenn Ihre Webseite den [!DNL Target] -Code ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) oder das [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)) implementiert, werden die Profilinformationen aus den Cookies mithilfe von Profilparametern an [!DNL Target] übergeben. [!DNL Target] identifiziert jeden Besucher eindeutig über einen `pcID`, den er in den Cookies des Besuchers generiert. Sie können Profilparameter jedoch mit `mbox3rdPartyIds` von einer externen App über Mbox-Aufrufe übergeben.

Verwenden Sie die [!DNL Adobe Target]-Profil-APIs, wenn Sie Profildaten zu Ihren Besuchern an [!DNL Target] senden möchten, die Sie im Rahmen Ihrer seitenbasierten Integration mit [!DNL Target] entweder nicht senden können oder nicht senden möchten. Dies können Daten aus einem CRM-System (Customer Relationship Management) oder POS-System (Point of Sale) sein, die nicht auf der Seite verfügbar sind. Oder diese Daten sind möglicherweise empfindlicher, sodass es nicht sinnvoll ist, sie auf der Seite weiterzugeben.

Es gibt zwei Möglichkeiten, Profile über API zu aktualisieren:

* [API zur Aktualisierung von einzelnen Profilen](/help/dev/administer/profile-api/profile-single-api.md)
* [Massenprofilaktualisierung über Batch](/help/dev/administer/profile-api/profile-bulk-api.md)
