---
keywords: Cloud-Instanzen, öffentliche Suffix-Liste, öffentliches Suffix, Cookie, Erstanbieter-Cookie, Erstanbieter-Cookie, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com,, cookieDomain, Cloud-Instanzen5, Cloud-Instanzen6, Cloud-Instanzen7, Cloud-Instanzen8, Cloud-Instanzen9, öffentliche Suffix-Liste0, öffentliche Suffix-Liste1, öffentliche Suffix-Liste2, öffentliche Suffix-Liste3, öffentliche Suffix-Liste4, öffentliche Suffix-Liste5
description: Erfahren Sie mehr über Probleme (mit Lösungen), auf die Kundinnen und Kunden stoßen, wenn sie Cloud [!DNL Adobe Target] basierte Instanzen zum Testen oder für Machbarkeitsprüfungen verwenden.
title: Kann ich  [!DNL Target]  mit Cloud-basierten Instanzen verwenden?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
TQID: https://experienceleague.adobe.com/df63sTQxukCfa4pYc1X6FRvxV3cY2UG-ixk5v9Fqh-c
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 46%

---

# Verwenden Cloud-basierter Instanzen mit [!DNL Target]

Informationen zu Problemen, die Kunden beim Verwenden Cloud-basierter Instanzen zum Testen von [!DNL Adobe Target] haben.

[!DNL Target]-Kunden verwenden mitunter Cloud-basierte Instanzen mit [!DNL Target] zum Testen oder für einfache Machbarkeitsprüfungen. Diese Instanzen umfassen möglicherweise die folgenden Domänen:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` oder `firebaseapp.com`.

Diese Domänen sind neben vielen anderen Teil der [öffentlichen Suffix-Liste](https://publicsuffix.org/list/public_suffix_list.dat).

**Problem:** Moderne Browser speichern keine Cookies, wenn Sie diese Domänen verwenden.

Die at.js-JavaScript-Bibliothek verwendet Cookies, um Benutzerinnen und Benutzer zu verfolgen und sicherzustellen, dass [!DNL [!DNL Target]] immer ein konsistentes Erlebnis bereitstellt. Wenn die [!DNL Target] JavaScript-Bibliothek keine Cookies speichern kann, werden Target-Anforderungen deaktiviert.

**Lösung:** Wenn Sie Cloud-basierte Instanzen mit in der öffentlichen Suffix-Liste enthaltenen Domänen verwenden möchten, hat es sich bewährt, die `cookieDomain`-Einstellung anzupassen. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).


