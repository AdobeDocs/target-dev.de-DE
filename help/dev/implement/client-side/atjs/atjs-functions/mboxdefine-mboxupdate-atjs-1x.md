---
keywords: mboxDefine, mboxDefine, mboxUpdate, mboxUpdate, mboxUpdate, mbox-Update, at.js, Funktionen, funktion, mboxDefine0
description: Verwenden Sie die Funktionen [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()] für die JavaScript-Bibliothek [!DNL Adobe Target] at.js , um eine Mbox zu definieren oder zu aktualisieren. (at.js 1.x)
title: Wie verwende ich die Funktionen [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()]?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 53%

---

# [!UICONTROL mboxDefine()] und [!UICONTROL mboxUpdate()] - at.js 1.x

Definieren und aktualisieren Sie eine Mbox in [!DNL Adobe Target].

>[!NOTE]
>
>Diese Funktionen stehen nur für at.js, Version 1.*x*, zur Verfügung. Diese Funktionen wurden mit der Veröffentlichung von at.js 2 nicht mehr unterstützt.*x*. Diese Funktionen geben Standardinhalte zurück, wenn sie mit at.js 2 verwendet werden.*x*.

`[!UICONTROL mboxDefine()]` und `[!UICONTROL mboxCreate()]` sind an „DIV“-HTML-Elemente gebunden, in denen das Angebot angezeigt werden soll. Diese Elemente sollten die Klasse `mboxDefault` aufweisen. Wenn diese Klasse nicht an die HTML-Elemente angefügt wird, tritt möglicherweise ein deutliches Flackern auf.

## mboxDefine 

Erstellt eine interne Zuordnung zwischen einer „nodeid“ und einem Mbox-Namen, führt die Anforderung jedoch nicht aus Die Funktion kommt in der Regel zusammen mit `[!UICONTROL mboxUpdate()]` zum Einsatz. Wird hauptsächlich in at.js integriert, um den Übergang von mbox.js (jetzt nicht mehr unterstützt) zu at.js zu erleichtern.

## mboxUpdate

Führt die Anforderung aus und wendet das Angebot auf das von `nodeId` in `mboxDefine()` () identifizierte Element an. Die Funktion kann auch dazu genutzt werden, eine Mbox zu aktualisieren, die durch `[!UICONTROL mboxCreate]` initiiert wurde. Wird hauptsächlich in at.js integriert, um den Übergang von mbox.js (jetzt nicht mehr unterstützt) zu at.js zu erleichtern. `mboxDefine()`/ `mboxUpdate()` kann mithilfe der Selektor-Option durch [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) und [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) ersetzt werden.

## Beispiel

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
