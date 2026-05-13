---
title: Profilaktualisierung
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten an  [!DNL Target] senden.
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/jclCuF4pe3JwAN-2RhQ9NfA5KtEfKUuawlmrE3aS0bQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 217
ht-degree: 3%

---

# Profilaktualisierung

Ein Benutzerprofil enthält demografische und Verhaltensinformationen eines Web-Seitenbesuchers, z. B. Alter, Geschlecht, gekaufte Produkte, letzte Besuchszeit und so weiter. [!DNL Adobe Target] verwendet diese Informationen, um den Inhalt für jeden Besucher zu personalisieren.

Die Profilinformationen für jeden Besucher werden entweder in Cookies oder in Apps von Drittanbietern gespeichert.

Wenn Ihre Web-Seite den [!DNL Target]-Code ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md) oder den [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)) implementiert, werden die Profilinformationen aus den Cookies mithilfe von Profilparametern an [!DNL Target] übergeben. [!DNL Target] identifiziert jeden Besucher eindeutig anhand einer `pcID`, die in den Cookies des Besuchers generiert wird. Sie können jedoch mithilfe von `mbox3rdPartyIds` Profilparameter aus einer externen App über Mbox-Aufrufe übergeben.

Verwenden Sie die [!DNL Adobe Target]-Profil-APIs, wenn Sie Profildaten über Ihre Besucher haben, die Sie im Rahmen Ihrer seitenbasierten Integration mit [!DNL Target] an [!DNL Target] senden können, die Sie nicht senden können oder möchten. Dabei kann es sich um Daten aus einem CRM (Customer Relationship Management)- oder POS (Point of Sale)-System handeln, die auf der Seite nicht verfügbar sind. Oder diese Daten sind möglicherweise sensibler, sodass es nicht sinnvoll ist, sie auf der Seite weiterzugeben.

Es gibt zwei Möglichkeiten, Profile über die API zu aktualisieren:

* [API zur Aktualisierung von einzelnen Profilen](/help/dev/administer/profile-api/profile-single-api.md)
* [Massenaktualisierung von Profilen über Batch](/help/dev/administer/profile-api/profile-bulk-api.md)
