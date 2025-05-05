---
keywords: Implementierung, at.js, Adobe Experience Platform Web SDK, AEP Web SDK
description: Erfahren Sie, wie Sie  [!DNL Adobe Target]  für Client-seitiges Web mit der  [!DNL Adobe Experience Platform Web SDK] AEP Web SDK) oder der JavaScript-Bibliothek at.js implementieren.
title: Wie implementiere ich  [!DNL Target]  Client-seitiges Web?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Übersicht: Implementieren von [!DNL Target] für clientseitiges Web

Bei Client-seitigen Implementierungen von [!DNL Adobe Target] stellt [!DNL Target] die mit einer Aktivität verknüpften Erlebnisse direkt dem Client-Browser bereit. Der Browser entscheidet, welches Erlebnis angezeigt werden soll, und zeigt es an. Bei einer Client-seitigen Implementierung können Sie einen WYSIWYG-Editor, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen.

Um [!DNL Target] Client-seitig zu implementieren, müssen Sie eine der folgenden JavaScript-Bibliotheken verwenden:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)

  Mit dem [!UICONTROL Adobe Experience Platform Web SDK] können Sie über die [!UICONTROL Adobe Experience Edge Network] mit den verschiedenen Services in der [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) interagieren. Wenn Sie sich für die Migration zum [!UICONTROL Adobe Experience Platform Web SDK] entscheiden, lesen Sie [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md)?

* [[!DNL Target] at.js-JavaScript-Bibliothek](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  Die at.js-JavaScript-Bibliothek sorgt für kürzere Seitenladezeiten bei Web-Implementierungen, höhere Sicherheit und bessere Implementierungsoptionen für Single Page Applications (SPA). Wenn Sie zu at.js migrieren möchten, lesen Sie [Funktionsweise von at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) und [[!DNL Adobe Target] Skill Builder: Developer Chat, migrieren Sie Adobe Targets mbox.js zu at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Unter [Vergleichen der at.js-Bibliothek mit der Web-SDK](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} erfahren Sie mehr über die Unterschiede zwischen den beiden Implementierungsansätzen.