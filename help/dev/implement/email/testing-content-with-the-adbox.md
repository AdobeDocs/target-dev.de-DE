---
keywords: Implementierung, Nicht-JavaScript, Mbox, AdBox
description: Verwenden Sie eine AdBox, um Bilder in einer Offsite-Implementierung mit  [!DNL Adobe Target] bereitzustellen. Eine AdBox ist wie eine Mbox, wird jedoch von einer URL anstelle von JavaScript gesteuert.
title: Wie erstelle ich eine AdBox für ein Bild?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 71%

---

# Erstellen einer AdBox für ein Bild

Verwenden Sie eine AdBox, um Bilder in einer Offsite-Implementierung mit [!DNL Adobe Target] bereitzustellen.

Eine AdBox funktioniert wie eine Mbox, wird aber mithilfe einer URL statt mit JavaScript gesteuert. AdBoxes werden mit einer speziellen AdBox-URL erstellt, die eine „Werbeanzeigen“-Mbox (oder AdBox) in Ihr Adobe-Konto lädt. Verwenden Sie diese AdBox anstelle der Mbox für Ihre Aktivitäten. Verwenden Sie die AdBox-URL anstelle eines direkten Bildverweises in E-Mail- oder anderen Nicht-JavaScript-Implementierungen.

Hilfe zur Auswahl der richtigen Einrichtung finden Sie unter [Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md).

1. Erstellen der AdBox-URL:

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * Bei `myClientCode` handelt es sich um den Clientcode Ihres Unternehmens. Der Clientcode Ihres Unternehmens enthält ausschließlich Kleinbuchstaben und keine Sonderzeichen.

     Ihr Clientcode ist oben auf der Seite **[!UICONTROL Administation]** > **[!UICONTROL Implementation]** der Benutzeroberfläche von [!DNL Target] verfügbar.

   * Bei `image` handelt es sich um den Aufruftyp. In diesem Fall handelt es sich um ein Bild.

   * Bei `emailHeroImage123_320x200` handelt es sich um den Namen der AdBox.

   * Bei `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` handelt es sich um den Standardinhalt der Mbox. Dabei muss es sich um ein Bild handeln.

     Hierbei muss es sich um einen URL-kodierten, absoluten Verweis handeln. Sie können die [HTML URL Encoding Reference](https://www.w3schools.com/tags/ref_urlencode.asp) verwenden, um Ihre URLs schnell zu kodieren.

1. Erstellen Sie [Weiterleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html) für alle alternativen Bilder.

   >[!NOTE]
   >
   >In AdBoxes muss ein Weiterleitungsangebot oder das standardmäßige Inhaltsangebot geladen sein. Andere Angebotstypen funktionieren nicht. Da es sich bei der AdBox um eine URL handelt, können nur die URLs angezeigt werden, die sie empfängt, weshalb nur die Weiterleitungsangebote funktionieren.

1. Erstellen Sie die Aktivität.

   Unter [Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md) finden Sie die richtigen Einstellungen, um Ihre Ziele zu erreichen.

1. Führen Sie die Qualitätssicherung für die Aktivität durch.

   Es hat sich bewährt, eine Platzhalter-Seite zu erstellen und sicherzustellen, dass alle Erlebnisse, Standardinhalte und Berichte wie erwartet in allen Browsern und für alle Ihre Umgebungen funktionieren.

1. Starten Sie die Aktivität.
