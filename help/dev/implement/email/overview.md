---
keywords: Implementierung, at.js, kein JavaScript, adbox, redirector, mbox
description: Erfahren Sie, wie  [!DNL Adobe Target]  in Nicht-JavaScript-Szenarien implementiert werden, z. B. mit einer AdBox oder einem Redirector.
title: Wie implementiere ich " [!DNL Target] " für E-Mail?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 63%

---

# E-Mail: [!DNL Target] implementieren

Informationen zur Implementierung von [!DNL Target] in Nicht-JavaScript-Szenarien, z. B. bei Verwendung einer AdBox oder eines Redirectors.

Sie können Besuche von Werbeanzeigen und anderen Offsite-Inhalten nachverfolgen. Darüber hinaus können Sie denselben Benutzer beim Besuchen und Verlassen Ihrer Site verfolgen und das gesamte Web-Erlebnis für ihn konsistent gestalten. Mit einer einzigen URL ermöglicht die AdBox Tests ohne JavaScript oder at.js.

Eine AdBox ist für Sites nützlich, die keine at.js haben, wie z. B. verbundene Unternehmen. Wenn für Ihre Aktivität dynamische Werbeinhalte benötigt werden (Sie also beispielsweise ein Produkt in der Werbeanzeige zeigen möchten, das im Warenkorb gelassen wurde), kann eine AdBox nicht verwendet werden.

AdBox-Anzeigen und Weiterleitungen können mit jeder beliebigen Aktivität verwendet werden. In der folgenden Tabelle werden AdBox und Weiterleitungen verglichen, und es wird angegeben, wann sie verwendet werden sollten:

| | Zielsetzung | Verwendungsbereiche | URL-Struktur | Angebotstyp | Angebotsinhalt |
|--- |--- |--- |--- |--- |--- |
| AdBox | Gibt verschiedene Bilder für die Werbeanzeige aus | Um die Inhalte einer Werbeanzeige zu ändern | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | Umleitungsangebot | URL für ein Bild |
| Weiterleitung | Leitet einen Besucher an eine andere Webseite weiter | Um die Landingpage einer Werbeanzeige zu ändern | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | Umleitungsangebot | URL für eine Seite |

## Best Practices für die Sicherheit

Beachten Sie, dass Sie bei Redirector einer Schwachstelle der Kategorie „Open Redirect“ ausgesetzt sein können. Zur Vermeidung einer unbefugten Nutzung von Weiterleitungs-Links durch Dritte empfehlen wir die Verwendung von „autorisierten Hosts“ zur Zulassungsliste der Domains der Standard-Weiterleitungs-URL. [!DNL Target] verwendet Hosts, um Domains auf die Zulassungsliste setzen, zu denen Umleitungen erlaubt sein sollen. Auf die Zulassungsliste setzen Weitere Informationen finden Sie unter [Erstellen von Hosts, die autorisiert sind, Mbox-Aufrufe an zu senden [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) in *Hosts*.

## Einschränkungen

* Es gibt keinen clientseitigen Timeout wie bei Standard-Mboxes. Wenn [!DNL Target] vollständig heruntergefahren ist, werden Besuchende der Anzeige keine Inhalte sehen, nicht einmal Standardinhalte.
* Die Besuche werden mithilfe von Drittanbieter-Cookies nachverfolgt. Unterscheiden sich die PCIDs, wird das Drittanbieterprofil des Besuchers standardmäßig mit bestehenden Erstanbieterprofilen zusammengeführt.
* Um Erstanbieter-Cookies für die AdBox selbst zu verwenden, müssen Sie die mBox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um Erstanbieter-Cookies zur Verfolgung von Werbeanzeigen-Klicks zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um mehr als eine AdBox auf derselben Seite zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema. Sie können eine AdBox und einen Weiterleitungslink auf derselben Seite haben (da es sich bei einer Weiterleitung eigentlich um eine zweite Seite handelt).
