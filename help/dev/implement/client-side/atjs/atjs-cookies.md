---
keywords: at.js, 2.0, 1.x, Cookies
description: Details zur [!DNL Adobe Target] at.js 2.x und at.js 1.x verarbeiten Cookies
title: Cookies in at.js
feature: at.js
exl-id: 154a844a-6855-4af7-8aed-0719b4c389f5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 77%

---

# „at.js“-Cookies

Informationen zum Cookie-Verhalten von at.js 2.x und at.js 1.*x*.

## Cookie-Verhalten von at.js 2.x

Für at.js Version 2.x (bis, jedoch nicht einschließlich Version 2.10.0), *Nur Erstanbieter-Cookies werden unterstützt*. Genau wie in at.js 1.*x*, wird das Erstanbieter-Cookie &quot;mbox&quot;unter `clientdomain.com`, wobei `clientdomain` ist Ihre Domäne.

at.js erzeugt eine Sitzungs-ID und speichert sie im Cookie. Die erste Antwort enthält alle Aktivitätsinformationen sowie die `TNT` oder `PC ID`, die von den [!DNL Target]-Servern generiert wurde. at.js fügt dann die `TNT/PC ID` zum Cookie hinzu.

Die `AMCV_###@AdobeOrg` Erstanbieter-Cookie wird immer vom Experience Cloud-ID-Dienst gesetzt, obwohl die Variable `ECID` wird übergeben [!DNL Target] -Anfragen.

>[!NOTE]
>
>Bei at.js-Versionen 2.10.0 und höher werden Erstanbieter- und domänenübergreifende Cookies unterstützt.

### Unterstützung für Drittanbieter-Cookies und domänenübergreifendes Tracking

Domänenübergreifendes Tracking ermöglicht die Anzeige von Sitzungen auf zwei verwandten Sites mit verschiedenen Domänen als einzelne Sitzung. Sie können eine [!DNL Target]-Aktivität erstellen, die sich über `siteA.com` und `siteB.com` erstreckt, während der Besucher im selben Erlebnis verbleibt, wenn er von einer Domain in die andere wechselt. Diese Funktionalität hängt mit at.js 1.*x* zusammen und damit, wie Erst- und Drittanbieter-Cookies behandelt werden.

>[!NOTE]
>
>Für at.js-Versionen 2.10.0 und höher werden sowohl Drittanbieter-Cookies als auch domänenübergreifendes Tracking unterstützt.


## at.js 1.*x*   Cookie-Verhalten

Für at.js 1.*x* ist das Verhalten von Cookies davon abhängig, ob es sich um ein Erstanbieter-Cookie, ein Drittanbieter-Cookie mit Erstanbieter-Cookie oder nur um ein Drittanbieter-Cookie handelt.

### Verwenden von Erstanbieter-Cookies und Drittanbieter-Cookies

Durch Ihre Site-Einrichtung wird bestimmt, welche Cookies Sie verwenden. Es ist hilfreich zu verstehen, wie [!DNL Target] funktioniert beim Versuch, Erstanbieter- und Drittanbieter-Cookies zu verstehen. Siehe [How [!DNL Adobe Target] works](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) für weitere Informationen.

Es gibt drei Haupt-Nutzungsszenarien für Cookies:

1. Eine Domain.

   Sämtliche Tests finden innerhalb einer Top-Level-Domain statt (z. B. `www.domain.com`, `store.domain.com`, `anysub.domain.com`).

   Verwenden Sie nur Erstanbieter-Cookies. Dies ist die Standardvorgehensweise.

1. Die Benutzer wechseln zwischen Domänen und Sie möchten ihr Verhalten auf allen diesen Domänen nachverfolgen und testen.

   Beispiel: Ein Benutzer besucht Ihren Onlineshop, geht aber über Yahoo Store zum Checkout. Drei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer die beste Vorgehensweise):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.
   * Nur Drittanbieter-Cookies aktivieren (sehr selten, doch der Vorteil ist, dass das at.js-Cookie von Ihrer Domain fern bleibt).
   * Nur Erstanbieter-Cookies aktivieren und den Parameter `mboxSession` beim Wechseln von Domänen weitergeben.

     Der Parameter `mboxSession` muss an eine Landingpage mit Verweis auf at.js übergeben werden. Es darf sich nicht um eine Zwischenseite als Weiterleitung handeln.

1. Sie verwenden nur AdBoxes oder Flashboxes auf einer Site eines Drittanbieters.

   Zwei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundendienst-Ansprechpartner die beste Vorgehensweise):

   * Erst- und Drittanbieter-Cookies aktivieren.

     Erst- und Drittanbieter-Cookies sind für Flashbox- und dynamische Kreativinhalte erforderlich.

   * Nur Drittanbieter-Cookies aktivieren.

     Diese Vorgehensweise wird nur in seltenen Fällen angewendet, in denen AdBox-Implementierungen ohne On-Site-Targeting verwendet werden.

### Verhalten von Erstanbieter-Cookies

Das Erstanbieter-Cookie wird unter `clientdomain.com` gespeichert, wobei `clientdomain` Ihre Domain ist.

at.js generiert eine `mboxSession ID` und speichert sie im Cookie. Die erste Antwort enthält das Angebot sowie das JavaScript, um die von der Anwendung erzeugte `mboxPC ID`-Kennung im Mbox-Cookie zu speichern.

>[!NOTE]
>
>Die `AMCV_###@AdobeOrg` Erstanbieter-Cookie wird immer mit der Experience Cloud-Besucher-ID gesetzt.

### Verhalten von Drittanbieter-Cookies

Das Drittanbieter-Cookie wird unter `clientcode.tt.omtrdc.net` und das Erstanbieter-Cookie unter `clientdomain.com` gespeichert, wobei `clientdomain` Ihre Domain ist.

at.js generiert eine `mboxSession ID`. Die erste Ortsanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Wenn der Browser Drittanbieter-Cookies ablehnt, enthält die Weiterleitungsanfrage diese Cookies nicht und es wird überall auf der Seite Standardinhalt angezeigt. Da keine Cookies eingerichtet wurden, wird bei jeder Seitenanfrage der gleiche Prozess ausgeführt.

### Verhalten von Drittanbieter- und Erstanbieter-Cookies

Das Drittanbieter-Cookie wird unter `clientcode.tt.omtrdc.net` und das Erstanbieter-Cookie unter `clientdomain.com` gespeichert, wobei `clientdomain` Ihre Domain ist.

at.js generiert eine `mboxSession ID`. Die erste Ortanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Einige Browser weisen Drittanbieter-Cookies ab. Wenn das Drittanbieter-Cookie blockiert wird, funktioniert das Erstanbieter-Cookie immer noch. [!DNL Target] versucht, das Drittanbieter-Cookie festzulegen. Falls dies nicht möglich ist, kann [!DNL Target] nur die spezifische Domain des Kunden nachverfolgen. Eine domänenübergreifende Nachverfolgung funktioniert nicht, wenn der Drittanbieter blockiert ist, es sei denn, die `mboxSession` ist an den domänenüberschreitenden Link angehängt. In diesem Fall wird ein weiteres Erstanbieter-Cookie gesetzt und mit dem Erstanbieter-Cookie der vorherigen Domain synchronisiert.

## Cookie-Einstellungen

Das Cookie verfügt über mehrere Standardeinstellungen. Sie können diese Einstellungen bei Bedarf ändern, außer die Cookie-Dauer. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie Cookie-Einstellungen ändern möchten.

| Einstellung | Informationen |
|--- |--- |
| Cookie-Name | mbox. |
| Cookie-Domäne | Die obersten und die darunter liegenden Ebenen der Domänen, von denen der Inhalt geliefert wird. Da die Belieferung von der Domain Ihres Unternehmens stattfindet, handelt es sich um ein Erstanbieter-Cookie. Beispiel: `mycompany.com`. |
| Serverdomäne | `clientcode.tt.omtrdc.net`, unter Verwendung des Kundencodes für Ihr Konto. |
| Cookie-Dauer | Das Cookie verbleibt zwei Jahre nach seiner letzten Anmeldung im Browser des Besuchers.<P>Die `deviceIdLifetime` -Einstellung überschrieben in [at.js , Version 2.3.1 oder neuer](../atjs/target-atjs-versions.md). Weitere Informationen finden Sie unter [targetGlobalSettings()](../../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md). |
| P3P-Richtlinie | Das Cookie wird mit einer P3P-Richtlinie veröffentlicht, wie sie von den Standardeinstellungen in den meisten Browsern gefordert wird. Durch eine P3P-Richtlinie wird einem Browser angezeigt, wer das Cookie bereitstellt und wie die Informationen verwendet werden. |

Das Cookie enthält verschiedene Werte, mit denen verwaltet werden kann, wie die Besucher die Kampagnen erleben:

| Wert | Definition |
|--- |--- |
| session ID | Eine eindeutige Kennung für eine Benutzersitzung. Standardmäßig ist diese 30 Minuten gültig. |
| pc ID | Eine eingeschränkt dauerhafte Kennung für den Browser eines Besuchers. Wird 14 Tage beibehalten. |
| check | Ein einfacher Testwert, mit dem bestimmt wird, ob ein Besucher Cookies unterstützt. Wird immer dann eingestellt, wenn ein Besucher eine Seite anfordert. |
| disable | Wird eingestellt, wenn die Ladezeit des Besuchers die im Adobe Experience Platform Web SDK oder in der Datei at.js konfigurierte Zeitüberschreitung überschreitet. Standardmäßig ist dieser Wert eine Stunde gültig. |

## Auswirkungen auf [!DNL Target] für Safari-Besucher aufgrund von Tracking-Änderungen in Apple WebKit

Berücksichtigen Sie Folgendes:

### Wie funktioniert [!DNL Adobe Target] Tracking der Arbeit?

| Cookies | Details |
|--- |--- |
| Erstanbieter-Domänen | Dies ist die Standardimplementierung für [!DNL Target] -Kunden.  Die „Mbox“-Cookies werden in der Domain des Kunden festgelegt. |
| Drittanbieter-Tracking | Das Tracking von Drittanbietern ist für Anwendungsfälle von Werbung und Targeting in [!DNL Target] und [!DNL Adobe Audience Manager] AAM.  Für das Drittanbieter-Tracking sind siteübergreifende Techniken zur Skripterstellung erforderlich.  [!DNL Target] verwendet zwei Cookies, „mboxSession“ und „mboxPC“, die in der Domain `clientcode.tt.omtrd.net` festgelegt sind. |

### Welchen Ansatz verfolgt Apple?

Von Apple (übersetzter Auszug):

„Intelligent Tracking Prevention ist eine neue WebKit-Funktion, die das siteübergreifende Tracking durch die Einschränkung von Cookies und anderen Website-Daten reduziert.“

„Das nennt man siteübergreifendes Tracking und das von `example-tracker.com` verwendete Cookie wird als Drittanbieter-Cookie bezeichnet. Im Rahmen unserer Tests haben wir beliebte Webseiten gefunden, die mehr als 70 solcher Tracker verwenden, die alle insgeheim Daten der Benutzer sammeln.“

| Ansatz | Details |
|--- |--- |
| Intelligent Tracking Prevention | Weitere Informationen finden Sie unter [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) auf der Website „WebKit Open Source Web Browser Engine“. |
| Cookies | Der Umgang mit Cookies in Safari:<ul><li>Drittanbieter-Cookies, die sich nicht auf einer Domain befinden, auf die der Benutzer direkt zugreift, werden nie gespeichert. Dieses Verhalten ist nicht neu. Drittanbieter-Cookies werden in Safari bereits nicht unterstützt.</li><li>Drittanbieter-Cookies, die auf einer Domain festgelegt sind, auf die der Benutzer direkt zugreift, werden nach 24 Stunden gelöscht.</li><li>Erstanbieter-Cookies werden nach 30 Tagen gelöscht, wenn die Klassifizierung der jeweiligen Erstanbieter-Domäne zeigt, dass Benutzer siteübergreifend verfolgt werden. Dies trifft möglicherweise auf große Unternehmen zu, die Benutzer online auf verschiedene Domänen weiterleiten. Apple hat sich bislang nicht dazu geäußert, wie genau solche Domänen klassifiziert werden oder wie eine Domain bestimmen kann, ob sie laut ihrer Klassifizierung Benutzer siteübergreifend verfolgt.</li></ul> |
| Maschinelles Lernen zur Identifikation von siteübergreifenden Domänen | Von Apple (übersetzter Auszug):<P>Machine Learning Classifier: Basierend auf den gesammelten Statistiken wird anhand eines maschinell lernenden Modells klassifiziert, welche privat registrierten Top-Level-Domains die Fähigkeit haben, Benutzer siteübergreifend zu verfolgen. Aus den zahlreichen gesammelten Statistiken haben sich drei Vektoren hervorgehoben, die einen starken Indikator für die Classification anhand aktueller Tracking-Vorgehensweisen darstellen: „Teilressource unter Anzahl der eindeutigen Domänen“, „Subframe unter Anzahl der eindeutigen Domänen“ und „Anzahl der eindeutigen Domänen weitergeleitet an“. Die gesamte Datensammlung und Classification erfolgt auf dem Gerät.<P>Interagiert ein Benutzer jedoch mit beispiel.com als Top-Level-Domäne, häufig auch als Erstanbieter-Domäne bezeichnet, wertet Intelligent Tracking Prevention dies als Zeichen dafür, dass der Benutzer an der Webseite interessiert ist und passt sein Verhalten vorübergehend wie in diesem Zeitstrahl dargestellt an:<P>Wenn der Benutzer in den letzten 24 Stunden mit example.com interagiert hat, sind seine Cookies verfügbar, wenn `example.com` ist ein Drittanbieter. Dies ermöglicht Anmeldeszenarien nach dem Schema „Mit meinem X-Konto bei Y anmelden“.<ul><li>Domänen, die als Top-Level-Domäne besucht werden, sind nicht betroffen. Seiten wie beispielsweise OKTA</li><li>Domänen, bei denen es sich um Sub-Domänen oder Subframes der aktuellen Seite handelt, werden über mehrere eindeutige Domänen hinweg identifiziert.</li></ul> |

### Wie wirkt sich das auf Adobe aus?

| Betroffene Funktionalität | Details |
|--- |--- |
| Abmeldeunterstützung | Wegen der durch das WebKit von Apple bewirkten Änderungen am Tracking ist die Unterstützung für Ausschlüsse hinfällig.<P>[!DNL Target] Opt-out verwendet ein Cookie im `clientcode.tt.omtrdc.net` Domäne. Weitere Informationen finden Sie unter [Datenschutz](/help/dev/before-implement/privacy/privacy.md).<P>[!DNL Target] unterstützt zwei Opt-outs:<ul><li>Einen pro Kunde (der Kunde verwaltet den Ausschluss-Link).</li><li>Eine über Adobe, die den Benutzer von allen abmeldet [!DNL Target] für alle Kunden.</li></ul>Beide Methoden verwenden den Drittanbieter-Cookie. |
| [!DNL Target] Aktivitäten | Kunden können ihre [Profillebensdauer](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) für ihre [!DNL Target] Konten - bis zu 90 Tage. Wenn die Profillebensdauer des Kontos länger als 30 Tage ist und das Erstanbieter-Cookie gelöscht wird, weil die Domäne des Kunden als Site-übergreifendes Tracking von Benutzern markiert wurde, besteht das Problem darin, dass das Verhalten von Safari-Besuchern in den folgenden Bereichen betroffen ist: [!DNL Target]:<P>**[!DNL Target]Berichte**: Wenn ein Safari-Benutzer eine Aktivität aufruft, nach 30 Tagen zurückkehrt und dann konvertiert, zählt dieser Benutzer als zwei Besucher und eine Konversion.<P>Dieses Verhalten ist für Aktivitäten mit [!DNL Analytics] als Berichtsquelle (A4T).<P>**Profil und Aktivitätsmitgliedschaft**:<ul><li>Profildaten werden gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li>Die Aktivitätsmitgliedschaft wird gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li> [!DNL Target] funktioniert in Safari nicht bei Konten, die eine Implementation mit Drittanbieter-Cookie oder Erst- und Drittanbieter-Cookie verwenden. Beachten Sie, dass es sich dabei nicht um ein neues Verhalten handelt. Safari erlaubt schon seit einer Weile keine Drittanbieter-Cookies.</li></ul><P>**Empfehlungen**: Wenn Bedenken bestehen, dass die Kundendomäne möglicherweise als eine Domäne markiert wird, die Besucher sitzungsübergreifend verfolgt, ist es am sichersten, die Profillebensdauer auf 30 Tage oder weniger in [!DNL Target]. So wird sichergestellt, dass Benutzer in Safari und allen anderen Browsern auf ähnliche Weise verfolgt werden. |
