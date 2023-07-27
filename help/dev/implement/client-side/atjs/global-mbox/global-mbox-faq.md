---
keywords: Fehlersuche, häufig gestellte Fragen, FAQ, FAQs, global, globale mbox
description: Häufig gestellte Fragen (FAQs) und Antworten zur Adobe lesen [!DNL Target] globale Mboxes.
title: Welche häufig gestellten Fragen beantworten die globale Mbox?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 60%

---

# Häufig gestellte Fragen zu globalen Mboxes

Liste der häufig gestellten Fragen (FAQs) zu globalen Mboxes.

## Kann ich mehr als eine globale Mbox haben, wenn meine [!DNL Target] -Konto über mehrere Domänen hinweg festgelegt ist?

Für Ihr Konto wird nur eine globale Mbox unterstützt.

Sie können den Ausführungsort Ihrer Aktivitäten beschränken, indem Sie Ihren Aktivitäten URL-Regeln hinzufügen. Weitere Informationen finden Sie unter [Gleiches Erlebnis auf ähnlichen Seiten](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Sie können auch mit [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) einen Parameter auf der Seite übergeben und dann diese Parameter im Abschnitt „URL konfigurieren“ im [!UICONTROL Visual Experience Composer][!UICONTROL  (VEC) auswählen. Alternativ können Sie die Parameter auch im formularbasierten Experience Composer als „Verfeinerungen“ hinzufügen].

## Wie übergebe ich Umsatzdaten an eine [!DNL Target] globale Mbox?

Um Umsatz- und Bestellinformationen in der target-global-mbox zu erfassen, müssen &quot;mbox-Parameter&quot;an [!DNL Target]. Diese Parameter sind Name/Wert-Paare, an die weitere Informationen gesendet werden [!DNL Target]. [!DNL Target] sucht diese Parameter (reservierte Namen) automatisch, um Umsatzdaten aufzufüllen.

Für die `orderConfirmPage` sollten Sie `orderTotal`, `orderId` und `productPurchasedId` weitergeben. 

Diese Parameter müssen an die target-global-mbox über `targetPageParams()`. Weitere Informationen finden Sie unter [Übergeben von Parametern an eine globale Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Sie möchten dem Konversionselement auch Targeting hinzufügen, damit [!DNL Target] zählt nur Konversionen auf der target-global-mbox, wenn die Bestellbestätigungsseite angezeigt wurde, wie unten dargestellt:

![ALT-Bild](assets/revenue1.png)

Der oben abgebildete Abschnitt „Webseiten“ enthält die folgenden Auswahlmöglichkeiten: „Aktuelle Seite“, „URL“, „contains“, „orderconfirm“.

![ALT-Bild](assets/revenue2.png)

Die Optionen in der oben gezeigten Abbildung umfassen die folgenden Einstellungen:

* **Was möchten Sie mit dieser Aktivität messen:** Umsatz
* **Standardansicht für Berichte:** Umsatz pro Besucher
* **Welche Aktion hat Ihre Zielgruppe ausgeführt, um anzugeben, dass Ihr Ziel erreicht wurde?** Anzeige einer mbox, target-global-mbox
