---
keywords: Fehlersuche, häufig gestellte Fragen, FAQ, FAQs, global, globale mbox
description: Lesen Sie häufig gestellte Fragen (FAQs) und Antworten zu Adobe [!DNL Target] globalen Mboxes.
title: Welche häufig gestellten Fragen beantworten die globale Mbox?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 43%

---

# Häufig gestellte Fragen zu globalen Mboxes

Liste der häufig gestellten Fragen (FAQs) zu globalen Mboxes.

## Kann ich mehr als eine globale Mbox haben, wenn mein [!DNL Target] -Konto domänenübergreifend festgelegt ist?

Für Ihr Konto wird nur eine globale Mbox unterstützt.

Sie können den Ausführungsort Ihrer Aktivitäten beschränken, indem Sie Ihren Aktivitäten URL-Regeln hinzufügen. Weitere Informationen finden Sie unter [Gleiches Erlebnis auf ähnlichen Seiten](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Sie können auch mit [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) einen Parameter auf der Seite übergeben und diese Parameter dann im Abschnitt &quot;URL konfigurieren&quot;im Abschnitt [!UICONTROL Visual Experience Composer] (VEC) auswählen oder die Parameter als &quot;Verfeinerungen&quot;im Abschnitt [!UICONTROL Form-Based Experience Composer] hinzufügen.

## Wie übergebe ich Umsatzdaten an eine globale Mbox mit [!DNL Target] .

Um Umsatz- und Bestellinformationen in der target-global-mbox zu erfassen, müssen &quot;mbox-Parameter&quot;an [!DNL Target] gesendet werden. Diese Parameter sind Name/Wert-Paare, mit denen weitere Informationen an [!DNL Target] gesendet werden. [!DNL Target] sucht automatisch nach diesen Parametern (reservierten Namen), um Umsatzdaten auszufüllen.

Für die `orderConfirmPage` sollten Sie `orderTotal`, `orderId` und `productPurchasedId` übergeben.

Diese Parameter müssen über `targetPageParams()` an die target-global-mbox gesendet werden. Weitere Informationen finden Sie unter [Übergeben von Parametern an eine globale Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Sie möchten außerdem das Targeting zum Konversionselement hinzufügen, sodass [!DNL Target] nur Konversionen auf der target-global-mbox zählt, wenn die Bestellbestätigungsseite angezeigt wurde, wie unten dargestellt:

![alt image](assets/revenue1.png)

Der oben abgebildete Abschnitt „Webseiten“ enthält die folgenden Auswahlmöglichkeiten: „Aktuelle Seite“, „URL“, „contains“, „orderconfirm“.

![alt image](assets/revenue2.png)

Die Optionen in der oben gezeigten Abbildung umfassen die folgenden Einstellungen:

* **Was möchten Sie mit dieser Aktivität messen:** Umsatz
* **Standardansicht für Berichte:** Umsatz pro Besucher
* **Welche Aktion hat Ihre Zielgruppe ausgeführt, um anzugeben, dass Ihr Ziel erreicht wurde?** Anzeige einer mbox, target-global-mbox
