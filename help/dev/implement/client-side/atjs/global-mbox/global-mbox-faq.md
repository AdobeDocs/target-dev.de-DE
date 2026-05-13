---
keywords: Fehlersuche, häufig gestellte Fragen, FAQ, FAQs, global, globale mbox
description: Lesen Sie häufig gestellte Fragen (FAQs) und Antworten zu Adobe [!DNL Target] globalen Mboxes.
title: Was sind häufig gestellte Fragen zur globalen Mbox?
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
TQID: https://experienceleague.adobe.com/bxsjCqSQpp6M20StzZtMBrfxjJCKgPEPfS2OlBUP00A
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 35%

---

# Häufig gestellte Fragen zu globalen Mboxes

Liste der häufig gestellten Fragen (FAQs) zu globalen Mboxes.

## Kann ich mehr als eine globale Mbox haben, wenn mein [!DNL Target]-Konto über mehrere Domains hinweg eingerichtet ist?

Für Ihr Konto wird nur eine globale Mbox unterstützt.

Sie können den Ausführungsort Ihrer Aktivitäten beschränken, indem Sie Ihren Aktivitäten URL-Regeln hinzufügen. Weitere Informationen finden Sie unter [Gleiches Erlebnis auf ähnlichen Seiten](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html).

Sie können auch mit [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) einen Parameter auf der Seite übergeben und diese Parameter dann im Abschnitt „URL konfigurieren“ im [!UICONTROL Visual Experience Composer] (VEC) auswählen oder indem Sie die Parameter im [!UICONTROL Form-Based Experience Composer] als „Verfeinerungen“ hinzufügen.

## Wie gebe ich Umsatzdaten an eine [!DNL Target] globale Mbox weiter?

Um Umsatz- und Bestellinformationen auf der target-global-mbox zu erfassen, müssen „mbox-Parameter“ an [!DNL Target] gesendet werden. Bei diesen Parametern handelt es sich um Name/Wert-Paare, die zum Senden weiterer Informationen an [!DNL Target] verwendet werden. [!DNL Target] sucht automatisch nach diesen Parametern (reservierte Namen), um Umsatzdaten auszufüllen.

Für die `orderConfirmPage` sollten Sie `orderTotal`, `orderId` und `productPurchasedId` übergeben.

Diese Parameter müssen über `targetPageParams()` an die target-global-mbox gesendet werden. Weitere Informationen finden Sie unter [Übergeben von Parametern an eine globale Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).

Es empfiehlt sich außerdem, dem Konversionsteil eine Zielgruppenbestimmung hinzuzufügen, sodass [!DNL Target] nur Konversionen auf der target-global-mbox zählt, wenn die Bestellbestätigungsseite aufgerufen wurde, wie unten dargestellt:

![ALT-Bild](assets/revenue1.png)

Der oben abgebildete Abschnitt „Webseiten“ enthält die folgenden Auswahlmöglichkeiten: „Aktuelle Seite“, „URL“, „contains“, „orderconfirm“.

![ALT-Bild](assets/revenue2.png)

Die Optionen in der oben gezeigten Abbildung umfassen die folgenden Einstellungen:

* **Was möchten Sie mit dieser Aktivität messen:** Umsatz
* **Standardansicht für Berichte:** Umsatz pro Besucher
* **Welche Aktion wurde von Ihrer Zielgruppe unternommen, um anzuzeigen, dass Ihr Ziel erreicht wurde?** hat eine mbox, target-global-mbox angezeigt
