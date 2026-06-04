---
keywords: Implementierung, at.js, Adobe Experience Platform Web SDK, AEP Web SDK
description: Erfahren Sie, wie Sie  [!DNL Adobe Target]  Client-seitiges Web mit der  [!DNL Adobe Experience Platform Web SDK] AEP Web SDK) oder der JavaScript-Bibliothek at.js implementieren.
title: Wie implementiere ich  [!DNL Target]  Client-seitiges Web?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
TQID: https://experienceleague.adobe.com/KgJyhvTguS8EXbwELaApI1mcs5egnEKHKpnxVYGqT4I
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 252
ht-degree: 26%

---

# Übersicht: Implementieren von [!DNL Target] für clientseitiges Web

Bei Client-seitigen Implementierungen von [!DNL Adobe Target] stellt [!DNL Target] die mit einer Aktivität verknüpften Erlebnisse direkt dem Client-Browser bereit. Der Browser entscheidet, welches Erlebnis angezeigt werden soll, und zeigt es an. Bei einer Client-seitigen Implementierung können Sie einen WYSIWYG-Editor, [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen.

Um [!DNL Target] Client-seitig zu implementieren, müssen Sie eine der folgenden JavaScript-Bibliotheken verwenden:

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  Mit [!UICONTROL Adobe Experience Platform Web SDK] können Sie über [!UICONTROL Adobe Experience Edge Network] mit den verschiedenen Services der [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) interagieren. Wenn Sie sich für die Migration zur [!UICONTROL Adobe Experience Platform Web SDK] entscheiden, lesen Sie [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md).

* [[!DNL Target] at.js-JavaScript-Bibliothek](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  Die at.js-JavaScript-Bibliothek sorgt für kürzere Seitenladezeiten bei Web-Implementierungen, höhere Sicherheit und bessere Implementierungsoptionen für Single Page Applications (SPA). Wenn Sie zu at.js migrieren möchten, lesen Sie [Funktionsweise von at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) und [[!DNL Adobe Target] Skill Builder: Developer Chat, migrieren Sie Adobe Targets mbox.js zu at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Unter [Vergleichen der at.js-Bibliothek mit der Web-SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) erfahren Sie mehr über die Unterschiede zwischen den beiden Implementierungsansätzen.
