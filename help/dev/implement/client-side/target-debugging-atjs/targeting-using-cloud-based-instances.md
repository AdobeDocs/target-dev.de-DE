---
keywords: Cloud-Instanzen, öffentliche Suffix-Liste, öffentliches Suffix, Cookie, Erstanbieter-Cookie, Erstanbieter-Cookie, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com,, targetGlobalSettings, cookieDomain, cloud instances5, cloud instances6, cloud instances7, cloud instances8, cloud instances9, public suffix list0, public suffix list1, public suffix list2, public , öffentliche Suffix list4, öffentliche Suffix list5
description: Erfahren Sie mehr über Probleme (mit Lösungen), mit denen Kunden konfrontiert sind, wenn sie Cloud-basierte Instanzen zum Testen von [!DNL Adobe Target] oder zu Machbarkeitszwecken verwenden.
title: Kann ich [!DNL Target] mit Cloud-basierten Instanzen verwenden?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 45%

---

# Verwenden Cloud-basierter Instanzen mit [!DNL Target]

Informationen zu Problemen, die Kunden beim Verwenden Cloud-basierter Instanzen zum Testen von [!DNL Adobe Target] haben.

[!DNL Target]-Kunden verwenden mitunter Cloud-basierte Instanzen mit [!DNL Target] zum Testen oder für einfache Machbarkeitsprüfungen. Diese Instanzen umfassen möglicherweise die folgenden Domänen:

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` oder `firebaseapp.com`.

Diese Domänen sind neben vielen anderen Teil der [öffentlichen Suffix-Liste](https://publicsuffix.org/list/public_suffix_list.dat).

**Problem:** Moderne Browser speichern keine Cookies, wenn Sie diese Domänen verwenden.

Die JavaScript-Bibliothek at.js verwendet Cookies zum Verfolgen von Benutzern, um sicherzustellen, dass [!DNL [!DNL Target]] stets ein konsistentes Erlebnis präsentiert. Wenn die JavaScript-Bibliothek [!DNL Target] keine Cookies speichern kann, werden Target-Anforderungen deaktiviert.

**Lösung:** Wenn Sie Cloud-basierte Instanzen mit in der öffentlichen Suffix-Liste enthaltenen Domänen verwenden möchten, hat es sich bewährt, die `cookieDomain`-Einstellung anzupassen. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
