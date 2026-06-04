---
keywords: Implementierung, nicht JavaScript, mbox, adbox
description: Verwenden Sie eine AdBox, um Bilder in einer Offsite-Implementierung mit bereitzustellen [!DNL Adobe Target]. Eine AdBox ist wie eine Mbox, wird aber von einer URL statt von JavaScript gesteuert.
title: Wie erstelle ich eine AdBox für ein Bild?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
TQID: https://experienceleague.adobe.com/OPo9T2Eb7afF8Ir8PAlY62OX83zhxtruUMKWCfUthxY
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 67%

---

# Erstellen einer AdBox für ein Bild

Verwenden Sie eine AdBox, um Bilder in einer Offsite-Implementierung mithilfe von [!DNL Adobe Target] bereitzustellen.

Eine AdBox funktioniert wie eine Mbox, wird aber mithilfe einer URL statt mit JavaScript gesteuert. AdBoxes werden mit einer speziellen AdBox-URL erstellt, die eine „Werbeanzeigen“-Mbox (oder AdBox) in Ihr Adobe-Konto lädt. Verwenden Sie diese AdBox anstelle der Mbox für Ihre Aktivitäten. Verwenden Sie die AdBox-URL anstelle eines direkten Bildverweises in E-Mail- oder anderen Nicht-JavaScript-Implementierungen.

Hilfe bei der Auswahl des richtigen Setups [&#x200B; Sie unter (Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md).

1. Erstellen der AdBox-URL:

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Bei `myClientCode` handelt es sich um den Clientcode Ihres Unternehmens. Der Clientcode Ihres Unternehmens enthält ausschließlich Kleinbuchstaben und keine Sonderzeichen.

     Der Client-Code ist oben auf der Seite **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** der [!DNL Target] verfügbar.

   * Bei `image` handelt es sich um den Aufruftyp. In diesem Fall handelt es sich um ein Bild.

   * Bei `emailHeroImage123_320x200` handelt es sich um den Namen der AdBox.

   * Bei `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` handelt es sich um den Standardinhalt der Mbox. Dabei muss es sich um ein Bild handeln.

     Hierbei muss es sich um einen URL-kodierten, absoluten Verweis handeln. Sie können die [HTML-URL-Codierungsreferenz](https://www.w3schools.com/tags/ref_urlencode.asp) verwenden, um Ihre URLs schnell zu codieren.

1. Erstellen Sie [Weiterleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html) für alle alternativen Bilder.

   >[!NOTE]
   >
   >In AdBoxes muss ein Weiterleitungsangebot oder das standardmäßige Inhaltsangebot geladen sein. Andere Angebotstypen funktionieren nicht. Da es sich bei der AdBox um eine URL handelt, können nur die URLs angezeigt werden, die sie empfängt, weshalb nur die Weiterleitungsangebote funktionieren.

1. Erstellen Sie die Aktivität.

   Unter [Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md) finden Sie die richtigen Einstellungen, um Ihre Ziele zu erreichen.

1. Führen Sie die Qualitätssicherung für die Aktivität durch.

   Es hat sich bewährt, eine Platzhalter-Seite zu erstellen und sicherzustellen, dass alle Erlebnisse, Standardinhalte und Berichte wie erwartet in allen Browsern und für alle Ihre Umgebungen funktionieren.

1. Starten Sie die Aktivität.
