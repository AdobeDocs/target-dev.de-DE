---
keywords: Implementierung, at.js Nicht-JavaScript, AdBox, Weiterleitung, Mbox
description: Erfahren Sie, wie Sie [!DNL Adobe Target] in Nicht-JavaScript-Szenarien implementieren, z. B. die Verwendung einer AdBox oder einer Weiterleitung.
title: Wie implementiere ich [!DNL Target] für E-Mail?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 63%

---

# E-Mail: Implementierung von [!DNL Target]

Informationen zur Implementierung von [!DNL Target] in Nicht-JavaScript-Szenarien, z. B. zur Verwendung einer AdBox oder Weiterleitung.

Sie können Besuche von Werbeanzeigen und anderen Offsite-Inhalten nachverfolgen. Darüber hinaus können Sie denselben Benutzer beim Besuchen und Verlassen Ihrer Site verfolgen und das gesamte Web-Erlebnis für ihn konsistent gestalten. Mithilfe einer einzelnen URL gestattet die AdBox das Testen ohne JavaScript oder at.js.

Eine AdBox ist nützlich für Sites ohne at.js, z. B. Partnersites. Wenn für Ihre Aktivität dynamische Werbeinhalte benötigt werden (Sie also beispielsweise ein Produkt in der Werbeanzeige zeigen möchten, das im Warenkorb gelassen wurde), kann eine AdBox nicht verwendet werden.

AdBox-Anzeigen und Weiterleitungen können mit jeder beliebigen Aktivität verwendet werden. In der folgenden Tabelle werden AdBox und Weiterleitungen verglichen, und es wird angegeben, wann sie verwendet werden sollten:

| | Zielsetzung | Verwendungsbereiche | URL-Struktur | Angebotstyp | Angebotsinhalt |
|--- |--- |--- |--- |--- |--- |
| AdBox | Gibt verschiedene Bilder für die Werbeanzeige aus | Um die Inhalte einer Werbeanzeige zu ändern | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | Umleitungsangebot | URL für ein Bild |
| Weiterleitung | Leitet einen Besucher an eine andere Webseite weiter | Um die Landingpage einer Werbeanzeige zu ändern | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | Umleitungsangebot | URL für eine Seite |

## Best Practices für die Sicherheit

Beachten Sie, dass Sie bei der Weiterleitung einem Risiko einer Open Redirect-Sicherheitslücke ausgesetzt sein können. Um die unbefugte Verwendung von Weiterleitungs-Links durch Dritte zu vermeiden, empfehlen wir die Verwendung von &quot;autorisierten Hosts&quot;, um die standardmäßigen Umleitungs-URL-Domänen in auf die Zulassungsliste setzen. [!DNL Target] verwendet Hosts zum Zulassungsliste von Domänen, zu denen Sie Umleitungen zulassen möchten. Weitere Informationen finden Sie unter [Erstellen von Zulassungslisten, die Hosts angeben, die Mbox-Aufrufe an  [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) senden dürfen, in *Hosts* .

## Einschränkungen

* Es gibt keinen clientseitigen Timeout wie bei Standard-Mboxes. Wenn [!DNL Target] vollständig ausfällt, sehen Besucher keine Inhalte der Anzeige, nicht einmal den Standard.
* Die Besuche werden mithilfe von Drittanbieter-Cookies nachverfolgt. Unterscheiden sich die PCIDs, wird das Drittanbieterprofil des Besuchers standardmäßig mit bestehenden Erstanbieterprofilen zusammengeführt.
* Um Erstanbieter-Cookies für die AdBox selbst zu verwenden, müssen Sie die mBox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um Erstanbieter-Cookies zur Verfolgung von Werbeanzeigen-Klicks zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um mehr als eine AdBox auf derselben Seite zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema. Sie können eine AdBox und einen Weiterleitungslink auf derselben Seite haben (da es sich bei einer Weiterleitung eigentlich um eine zweite Seite handelt).
