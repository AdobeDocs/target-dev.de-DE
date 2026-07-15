---
keywords: mboxDefine, mboxDefine, mboxDefine, mboxUpdate, mboxUpdate, mboxUpdate, at.js, features, function, mboxDefine0
description: Verwenden Sie die Funktionen [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()] für die JavaScript-Bibliothek  [!DNL Adobe Target] .at.js, um eine Mbox zu definieren oder zu aktualisieren. (at.js 1.x)
title: Wie verwende ich die Funktionen [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()]?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a1af9d2c909d9b3d506dd4875d1bd75149dbf636
workflow-type: tm+mt
source-wordcount: 208
ht-degree: 46%

---

# [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()] - at.js 1.x

Definieren und Aktualisieren einer Mbox in [!DNL Adobe Target].

>[!NOTE]
>
>Diese Funktionen sind nur für at.js-Versionen 1.*x* verfügbar. Diese Funktionen wurden mit der Veröffentlichung von at.js 2.*x* eingestellt. Diese Funktionen geben Standardinhalte zurück, wenn sie mit at.js 2.*x* verwendet werden.

`[!UICONTROL mboxDefine()]` und `[!UICONTROL mboxCreate()]` sind an „DIV“-HTML-Elemente gebunden, in denen das Angebot angezeigt werden soll. Diese Elemente sollten die Klasse `mboxDefault` aufweisen. Wenn diese Klasse nicht an die HTML-Elemente angefügt wird, tritt möglicherweise ein deutliches Flackern auf.

## mboxDefine

Erstellt eine interne Zuordnung zwischen einer „nodeid“ und einem Mbox-Namen, führt die Anforderung jedoch nicht aus Die Funktion kommt in der Regel zusammen mit `[!UICONTROL mboxUpdate()]` zum Einsatz. In at.js integriert, um vor allem den Übergang von mbox.js (inzwischen nicht mehr unterstützt) zu at.js zu erleichtern.

## mboxUpdate

Führt die Anforderung aus und wendet das Angebot auf das von `nodeId` in `mboxDefine()` () identifizierte Element an. Die Funktion kann auch dazu genutzt werden, eine Mbox zu aktualisieren, die durch `[!UICONTROL mboxCreate]` initiiert wurde. In at.js integriert, um vor allem den Übergang von mbox.js (inzwischen nicht mehr unterstützt) zu at.js zu erleichtern. `mboxDefine()`/ `mboxUpdate()` kann mithilfe der Selektor-Option durch [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) und [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) ersetzt werden.

## Beispiel

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```



