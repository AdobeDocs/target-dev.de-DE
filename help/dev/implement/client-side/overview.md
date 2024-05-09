---
keywords: Implementierung, at.js, Adobe Experience Platform Web SDK, aep Web SDK
description: Erfahren Sie, wie Sie [!DNL Adobe Target] für Client-seitige Webanwendungen mit dem [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) oder der JavaScript-Bibliothek at.js .
title: Implementieren [!DNL Target] für Client-seitiges Web
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Übersicht: Implementierung [!DNL Target] für Client-seitige Websites

Bei Client-seitigen Implementierungen von [!DNL Adobe Target] stellt [!DNL Target] die mit einer Aktivität verknüpften Erlebnisse direkt dem Client-Browser bereit. Der Browser entscheidet, welches Erlebnis angezeigt werden soll, und zeigt es an. Bei einer Client-seitigen Implementierung können Sie einen WYSIWYG-Editor, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen.

Zu implementieren [!DNL Target] clientseitig müssen Sie eine der folgenden JavaScript-Bibliotheken verwenden:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)

  Die [!UICONTROL Adobe Experience Platform Web SDK] ermöglicht die Interaktion mit den verschiedenen Diensten im [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) durch die [!UICONTROL Adobe Experience Edge Network]. Wenn Sie sich für eine Migration zum [!UICONTROL Adobe Experience Platform Web SDK], siehe [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] JavaScript-Bibliothek &quot;at.js&quot;](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  Die JavaScript-Bibliothek at.js verbessert die Seitenladezeiten bei Webimplementierungen, verbessert die Sicherheit und bietet bessere Implementierungsoptionen für Einzelseitenanwendungen. Informationen zum Migrieren zu at.js finden Sie unter [Funktionsweise von &quot;at.js&quot;](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) und [[!DNL Adobe Target] Skill Builder: Entwickler-Chat, Migration von Adobe Targets mbox.js zu at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Siehe [Vergleich der &quot;at.js&quot;-Bibliothek mit dem Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} , um mehr über die Unterschiede zwischen den beiden Implementierungsansätzen zu erfahren.