---
keywords: Implementierung, at.js, Adobe Experience Platform Web SDK, aep Web SDK
description: Erfahren Sie, wie Sie [!DNL Adobe Target] für Client-seitiges Web mit der JavaScript-Bibliothek "at.js"oder dem [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) implementieren.
title: Implementieren von [!DNL Target] für Client-seitiges Web
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Übersicht: Implementierung von [!DNL Target] für Client-seitiges Web

Bei Client-seitigen Implementierungen von [!DNL Adobe Target] stellt [!DNL Target] die mit einer Aktivität verknüpften Erlebnisse direkt dem Client-Browser bereit. Der Browser entscheidet, welches Erlebnis angezeigt werden soll, und zeigt es an. Bei einer Client-seitigen Implementierung können Sie einen WYSIWYG-Editor, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen.

Zur Client-seitigen Implementierung von [!DNL Target] müssen Sie eine der folgenden JavaScript-Bibliotheken verwenden:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)

  Mit dem [!UICONTROL Adobe Experience Platform Web SDK] können Sie mit den verschiedenen Diensten im [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) über den [!UICONTROL Adobe Experience Edge Network] interagieren. Wenn Sie sich für eine Migration zum [!UICONTROL Adobe Experience Platform Web SDK] entscheiden, finden Sie weitere Informationen unter [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [JavaScript-Bibliothek &quot;at.js&quot;[!DNL Target]](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  Die JavaScript-Bibliothek at.js verbessert die Seitenladezeiten für Webimplementierungen, verbessert die Sicherheit und bietet bessere Implementierungsoptionen für Einzelseitenanwendungen. Wenn Sie sich für eine Migration zu at.js entscheiden, finden Sie weitere Informationen unter [Funktionsweise von at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) und [[!DNL Adobe Target] Skill Builder: Entwickler-Chat, migrieren Sie die Adobe Target-mbox.js zu at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Informationen zu den Unterschieden zwischen den beiden Implementierungsansätzen finden Sie unter [Vergleichen der at.js-Bibliothek mit dem Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} .