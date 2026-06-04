---
keywords: Implementierung, at.js, kein JavaScript, adbox, redirector, mbox
description: Erfahren Sie, wie  [!DNL Adobe Target]  in Nicht-JavaScript-Szenarien implementiert werden, z. B. mit einer AdBox oder einem Redirector.
title: Wie implementiere ich " [!DNL Target] " für E-Mail?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
TQID: https://experienceleague.adobe.com/NeITIa97pW-yiB6EB-ajqRuBgp9mx-uzdwlREdgotj8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: c94a34eb-b51c-4dd1-a6a4-46b0d84ccccd
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 441
ht-degree: 62%

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

Beachten Sie, dass Sie bei Redirector einer Schwachstelle der Kategorie „Open Redirect“ ausgesetzt sein können. Zur Vermeidung einer unbefugten Nutzung von Weiterleitungs-Links durch Dritte empfehlen wir die Verwendung von „autorisierten Hosts“ zur Zulassungsliste der Domains der Standard-Weiterleitungs-URL. [!DNL Target] verwendet Hosts, um Domains auf die Zulassungsliste setzen, zu denen Umleitungen erlaubt sein sollen. Weitere Informationen finden Sie unter [Erstellen von Hosts, die autorisiert sind, Mbox-Aufrufe an zu senden [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) in *Hosts*.

## Einschränkungen

* Es gibt keinen clientseitigen Timeout wie bei Standard-Mboxes. Wenn [!DNL Target] vollständig heruntergefahren ist, werden Besuchende der Anzeige keine Inhalte sehen, nicht einmal Standardinhalte.
* Die Besuche werden mithilfe von Drittanbieter-Cookies nachverfolgt. Unterscheiden sich die PCIDs, wird das Drittanbieterprofil des Besuchers standardmäßig mit bestehenden Erstanbieterprofilen zusammengeführt.
* Um Erstanbieter-Cookies für die AdBox selbst zu verwenden, müssen Sie die mBox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um Erstanbieter-Cookies zur Verfolgung von Werbeanzeigen-Klicks zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema.
* Um mehr als eine AdBox auf derselben Seite zu verwenden, müssen Sie die Mbox-Sitzung in die URL aufnehmen. Ihr Kundenbetreuer gibt Ihnen gerne weiterführende Informationen zu diesem Thema. Sie können eine AdBox und einen Weiterleitungslink auf derselben Seite haben (da es sich bei einer Weiterleitung eigentlich um eine zweite Seite handelt).
