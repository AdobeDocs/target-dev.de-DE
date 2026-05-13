---
keywords: Implementierung, mbox.js-Nicht-JavaScript, Weiterleitung, Kosten pro Klick, Umsatz pro Klick
description: Erfahren Sie, wie Sie in E-Mail-Implementierungen Weiterleitungen verwenden, ähnlich wie bei der Verwendung einer Mbox in Ihren - [!DNL Adobe Target] .
title: Wie arbeite ich mit Weiterleitungen?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
TQID: https://experienceleague.adobe.com/3SUsZl1y9tk97sWgdB3iB7wrAXNb2LfN3hObJM14caE
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
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 689
ht-degree: 63%

---

# Arbeiten mit Weiterleitungen

Verwenden Sie eine Weiterleitung auf ähnliche Weise, wie Sie eine Mbox für Ihre Tests verwenden.

Weiterleitungen werden mit einer speziellen Weiterleitungs-URL erstellt, die eine Weiterleitungs-Mbox (Weiterleitung) in Ihr Konto lädt. Verwenden Sie diese Weiterleitung auf ähnliche Weise, wie Sie eine Mbox für Ihre Tests verwenden. Senden Sie die Weiterleitungs-URL als Ziel-Link der Werbung an Ihr Werbenetzwerk.

Verwenden Sie den Redirector für Folgendes:

* Klicks von Ihren Display-Anzeigen auf Ihre Seite zu verfolgen
* Einen einzigen, zentralisierten Bericht zur Verfolgung von Klicks auf Display-Anzeigen in mehreren Werbenetzwerken zu erstellen
* Die Display-Anzeigen und Ziele zu variieren

  Beispielsweise kann dasselbe Banner auf Ihre Startseite, Kategorieseite oder Produktseite verweisen.

* Finden Sie heraus, welche Landingpage die meisten Konversionen bringt.

Hilfe bei der Entscheidung über die richtige Einrichtung [&#x200B; Sie unter (Nicht-JavaScript-basierte Implementierungen](/help/dev/implement/email/overview.md).

## Erstellen eines Redirectors

Bevor Sie eine Weiterleitung verwenden können, müssen Sie diese erst erstellen.

1. Legen Sie die Zielort-Variationen für die Werbeanzeige fest, inklusive Standard-Zielposition.
1. Erstellen Sie die Weiterleitungs-URL.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * Bei `yourclientcode` handelt es sich um den Clientcode Ihres Unternehmens. Der Clientcode Ihres Unternehmens enthält ausschließlich Kleinbuchstaben und keine Sonderzeichen.

     Der Client-Code ist oben auf der Seite **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** der [!DNL Target]-Benutzeroberfläche verfügbar.

   * `redirectorlink_456` ist der Name der Weiterleitungs-mbox, die in Ihrem Konto zur Verwendung für Kampagnen und Tests angezeigt wird.

     Weiterleitungen funktionieren anders als andere Mboxes, erscheinen in Ihrem Konto aber so wie beliebige andere Mboxes. Benennen Sie die Weiterleitung so, dass sie sich einfach von den Standard-Mboxes in Ihrem Konto unterscheiden lässt.  Es hat sich bewährt, den Mbox-Namen mit „redirectorlink“ beginnen zu lassen.

   * `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` ist das Standardziel.

     Hierbei muss es sich um einen URL-kodierten, absoluten Verweis handeln. Sie können die [HTML-URL-Codierungsreferenz](https://www.w3schools.com/tags/ref_urlencode.asp) verwenden, um Ihre URLs schnell zu codieren.

   >[!WARNING]
   >
   >Beachten Sie, dass Sie mit Redirector einem Risiko für eine Open Redirect-Schwachstelle ausgesetzt sein können. Zur Vermeidung einer unbefugten Nutzung von Weiterleitungs-Links durch Dritte empfiehlt Adobe die Verwendung von „autorisierten Hosts“ zur Zulassungsliste der Domains der Standard-Weiterleitungs-URL. [!DNL Target] verwendet Hosts, um Domains auf die Zulassungsliste setzen, zu denen Umleitungen erlaubt sein sollen. Weitere Informationen finden Sie unter [Erstellen von Hosts, die autorisiert sind, Mbox-Aufrufe an zu senden [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de#allowlist) in *Hosts*.

1. Validieren Sie die Weiterleitung.
   1. *Best Practice für die Sicherheit*: Stellen Sie sicher, dass die im Redirector verwendete Domain wie oben angegeben auf die Zulassungsliste gesetzt ist. Wenn Sie eine Domain verwenden, die nicht auf die Zulassungsliste gesetzt ist, blockiert Adobe alle Aufrufe an diese Domain, um böswillige Akteure daran zu hindern, den Redirector zu verwenden, um zu potenziell böswilligen Domains umzuleiten.
   2. Fügen Sie die Weiterleitungs-URL in eine Browserzeile ein, und aktualisieren Sie den Browser.
   3. Melden Sie sich bei Ihrem Konto an, aktualisieren Sie Ihre Mbox-Liste, und überprüfen Sie, ob die neue Weiterleitung als Mbox aufgelistet wird.
1. Um verschiedene Ziele für eine Anzeige zu testen, erstellen Sie [Weiterleitungsangebote](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html?lang=de) für jede Version.
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
   >Weiterleitungen werden von der Angebotsvorschau oder Mbox-Suche nicht unterstützt. Zeigen Sie eine Vorschau der Erlebnisse direkt in einem Browser an. Außerdem funktioniert `mboxDebug` nicht mit Weiterleitungen.

1. Senden Sie die vollständige Weiterleitungs-URL als Zielort der Display-Anzeige an Ihr Display-Anzeigenetzwerk.

## Weiterleitung verwenden, um Kosten pro Klick und Umsatz pro Klick weiterzugeben

Informationen zum Verwenden einer Weiterleitung zum Übergeben der Kosten pro Klick und vom Umsatz pro Klick.

### Übergeben der Kosten pro Klick

Verwenden Sie eine Weiterleitung, um die Kosten pro Klick weiterzugeben.

>[!NOTE]
>
>Best Practice ist es, den Kostenwert mithilfe der **[!UICONTROL Score per visit]** Interaktionsmetrik zu bestimmen.

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
>Best Practice ist es, den Umsatzwert mithilfe der Metrik Interaktion mit **[!UICONTROL Score per visit]** zu bestimmen.

Fügen Sie `&mboxPageValue=value` zur URL hinzu.

Beispiel: Für Umsatz pro Klick in Höhe von 0,10 Cent.

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
