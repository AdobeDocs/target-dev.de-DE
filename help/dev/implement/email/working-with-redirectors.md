---
keywords: Implementierung, mbox.js-Nicht-JavaScript, Weiterleitung, Kosten pro Klick, Umsatz pro Klick
description: Erfahren Sie, wie Sie Weiterleitungen in E-Mail-Implementierungen ähnlich wie eine Mbox in Ihrer [!DNL Adobe Target] Aktivitäten.
title: Wie arbeite ich mit Weiterleitungen?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 69%

---

# Arbeiten mit Weiterleitungen

Verwenden Sie eine Weiterleitung auf ähnliche Weise, wie Sie eine Mbox für Ihre Tests verwenden.

Weiterleitungen werden mit einer speziellen Weiterleitungs-URL erstellt, die eine Weiterleitungs-Mbox (Weiterleitung) in Ihr Konto lädt. Verwenden Sie diese Weiterleitung auf ähnliche Weise, wie Sie eine Mbox für Ihre Tests verwenden. Senden Sie die Weiterleitungs-URL als Ziel-Link der Werbung an Ihr Werbenetzwerk.

Verwenden Sie die Weiterleitung, um  folgende Aktionen auszuführen:

* Klicks von Ihren Display-Anzeigen auf Ihre Seite zu verfolgen
* Einen einzigen, zentralisierten Bericht zur Verfolgung von Klicks auf Display-Anzeigen in mehreren Werbenetzwerken zu erstellen
* Die Display-Anzeigen und Ziele zu variieren

  Beispielsweise kann dasselbe Banner auf Ihre Startseite, Kategorieseite oder Produktseite verweisen.

* Finden Sie heraus, welche Landingpage die meisten Konversionen bringt.

Hilfe zur Entscheidung über die richtigen Einstellungen finden Sie unter  [Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md).

## Erstellen einer Weiterleitung

Bevor Sie eine Weiterleitung verwenden können, müssen Sie diese erst erstellen.

1. Legen Sie die Zielort-Variationen für die Werbeanzeige fest, inklusive Standard-Zielposition.
1. Erstellen Sie die Weiterleitungs-URL.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Bei `yourclientcode` handelt es sich um den Clientcode Ihres Unternehmens. Der Clientcode Ihres Unternehmens enthält ausschließlich Kleinbuchstaben und keine Sonderzeichen.

     Ihr Client-Code ist oben im **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** der [!DNL Target] -Schnittstelle.

   * `redirectorlink_456` ist der Name der Weiterleitungs-mbox, die in Ihrem Konto zur Verwendung für Kampagnen und Tests angezeigt wird.

     Weiterleitungen funktionieren anders als andere Mboxes, erscheinen in Ihrem Konto aber so wie beliebige andere Mboxes. Benennen Sie die Weiterleitung so, dass sie sich einfach von den Standard-Mboxes in Ihrem Konto unterscheiden lässt.  Es hat sich bewährt, den Mbox-Namen mit „redirectorlink“ beginnen zu lassen.

   * `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` ist das Standardziel.

     Hierbei muss es sich um einen URL-kodierten, absoluten Verweis handeln. Sie können die [HTML URL-Kodierungsreferenz](https://www.w3schools.com/tags/ref_urlencode.asp) um Ihre URLs schnell zu kodieren.

   >[!WARNING]
   >
   >Beachten Sie, dass Sie bei der Weiterleitung einem Risiko einer Open Redirect-Schwachstelle ausgesetzt sein können. Um die unbefugte Verwendung von Weiterleitungs-Links durch Dritte zu vermeiden, empfiehlt Adobe die Verwendung von &quot;autorisierten Hosts&quot;zur Zulassungsliste der standardmäßigen Umleitungs-URL-Domänen. [!DNL Target] verwendet Hosts, um Domains auf die Zulassungsliste zu setzen, für die Umleitungen erlaubt sind. Weitere Informationen finden Sie im Abschnitt [Hosts unter  [!DNL Target]Erstellen von Zulassungslisten mit Hosts, die autorisiert sind, Mbox-Aufrufe an](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist)*zu senden*.

1. Validieren Sie die Weiterleitung.
   1. *Best Practices für die Sicherheit*: Stellen Sie sicher, dass die in der Weiterleitung verwendete Domäne auf die Zulassungsliste gesetzt ist, wie oben angegeben. Wenn Sie eine Domäne verwenden, die nicht auf die Zulassungsliste gesetzt ist, blockiert Adobe alle Aufrufe an diese Domäne, um zu verhindern, dass böswillige Akteure die Weiterleitung verwenden, um zu potenziell bösartigen Domänen umzuleiten.
   2. Fügen Sie die Weiterleitungs-URL in eine Browserzeile ein, und aktualisieren Sie den Browser.
   3. Melden Sie sich bei Ihrem Konto an, aktualisieren Sie Ihre Mbox-Liste, und überprüfen Sie, ob die neue Weiterleitung als Mbox aufgelistet wird.
1. Um verschiedene Ziele für eine Anzeige zu testen, erstellen Sie [Weiterleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html) für jede Version.
1. Erstellen Sie die Kampagne.

   Unter [Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md) finden Sie die richtigen Einstellungen, um Ihre Ziele zu erreichen.
1. Führen Sie die Qualitätssicherung für die Kampagne durch.

   Erstellen Sie eine Platzhalterseite mit einem `<a href>`, der die Weiterleitungs-URL enthält. Beispiel:

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. Überprüfen Sie, ob alle Erlebnisse, Standardinhalte und Berichte wie erwartet in allen Browsern und für alle Ihre Umgebungen funktionieren.

   >[!NOTE]
   >
   >Weiterleitungen werden von der Angebotsvorschau oder Mbox-Suche nicht unterstützt. Zeigen Sie eine Vorschau der Erlebnisse direkt in einem Browser an. Außerdem `mboxDebug` funktioniert nicht mit Weiterleitungen.

1. Senden Sie die vollständige Weiterleitungs-URL als Zielort der Display-Anzeige an Ihr Display-Anzeigenetzwerk.

## Verwenden einer Weiterleitung, um Kosten pro Klick und Umsatz pro Klick weiterzugeben

Informationen zum Verwenden einer Weiterleitung zum Übergeben der Kosten pro Klick und vom Umsatz pro Klick.

### Übergeben der Kosten pro Klick

Verwenden Sie eine Weiterleitung, um die Kosten pro Klick weiterzugeben.

>[!NOTE]
>
>Best Practice ist, den Kostenwert mithilfe der **[!UICONTROL Ergebnis pro Besuch]** Interaktionsmetrik.

Fügen Sie `&mboxPageValue=-value` zur URL hinzu. Beachten Sie den Negativwert.

Beispiel: Für Kosten pro Klick in Höhe von 0,10 Cent:

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### Übergeben vom Umsatz pro Klick 

Verwenden Sie eine Weiterleitung, um den Umsatz pro Klick weiterzugeben.

>[!NOTE]
>
>Best Practice ist, den Umsatzwert mithilfe der Variablen **[!UICONTROL Ergebnis pro Besuch]** Interaktionsmetrik.

Fügen Sie `&mboxPageValue=value` zur URL hinzu.

Beispiel: Für Umsatz pro Klick in Höhe von 0,10 Cent.

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
