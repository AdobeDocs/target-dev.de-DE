---
keywords: Übersicht und Referenz, WebKit, Cookies, Erstanbieter, Drittanbieter, Erstanbieter, Drittanbieter, Drittanbieter, 8 $
description: Erfahren Sie mehr über das Verhalten von Target-Cookies (Erstanbieter-Cookie, Drittanbieter-Cookie mit Erstanbieter-Cookie oder Drittanbieter-Cookie allein).
title: Wo finde ich Informationen über Target-Cookies?
feature: at.js
role: Developer
source-git-commit: 39f390a0e5eedf8c6957333759d31d96ed11b321
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 53%

---

# Cookies in Target

Das Verhalten von Cookies ist davon abhängig, ob es sich um ein Erstanbieter-Cookie, ein Drittanbieter-Cookie mit Erstanbieter-Cookie oder nur um ein Drittanbieter-Cookie handelt.

>[!NOTE]
>
>Dieses Thema enthält Informationen zu `mboxSession` und `mboxPC`. Best Practices für die Implementierung empfehlen, keine vertraulichen Informationen mit den Cookie-Daten zu verknüpfen oder zu speichern: `mboxSession` oder `mboxPC`.

Siehe auch [Löschen des Target-](/help/dev/before-implement/privacy/cookie-deleting.md).

## Verwenden von Erstanbieter-Cookies und Drittanbieter-Cookies

Durch Ihre Site-Einrichtung wird bestimmt, welche Cookies Sie verwenden. Um Erstanbieter- und Drittanbieter-Cookies zu verstehen, ist es hilfreich, die Funktionsweise von Target zu verstehen. Weitere Informationen finden [&#x200B; unter &#x200B;](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=de) von Adobe Target .

Es gibt drei Haupt-Nutzungsszenarien für Cookies:

1. Eine Domain.

   Alle Ihre Tests finden innerhalb einer Domain auf oberster Ebene statt (`www.domain.com`, `store.domain.com`, `anysub.domain.com` usw.).

   Ansatz: Nur Erstanbieter-Cookies verwenden (Standard).

1. Die Benutzer wechseln zwischen Domänen und Sie möchten ihr Verhalten auf allen diesen Domänen nachverfolgen und testen.

   Beispiel: Ein Benutzer besucht Ihren Onlineshop, geht aber über Yahoo Store zum Checkout. Drei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer die beste Vorgehensweise):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.
   * Nur Drittanbieter-Cookies aktivieren (selten, doch der Vorteil ist, dass das mbox-Cookie von Ihrer Domain fern bleibt).
   * Nur Erstanbieter-Cookies aktivieren und den Parameter `mboxSession` beim Wechseln von Domänen weitergeben.

     Der `mboxSession` muss an eine Landingpage übergeben und von der JavaScript-Bibliothek (Adobe Experience Platform Web SDK oder at.js) referenziert werden. Es darf sich nicht um eine Zwischenseite als Weiterleitung handeln.

1. Sie verwenden nur AdBoxes oder Flashboxes auf einer Site eines Drittanbieters.

   Zwei Ansätze (Bestimmen Sie gemeinsam mit Ihrem Kundenbetreuer den besten Ansatz):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.

     Erstanbieter- und Drittanbieter-Cookies sind für Flashbox- und dynamische Kreativinhalte erforderlich.

   * Nur Drittanbieter-Cookies aktivieren.

     Diese Vorgehensweise wird nur in seltenen Fällen angewendet, in denen AdBox-Implementierungen ohne On-Site-Targeting verwendet werden.

## Verhalten von Erstanbieter-Cookies

Das Erstanbieter-Cookie wird unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert ein `mboxSession ID` und speichert es im Target-Cookie. Die erste Mbox-Antwort enthält das Angebot und die JavaScript zum Speichern der von der Anwendung generierten `mboxPC ID` im Mbox-Cookie .

>[!NOTE]
>
>Das AMCV_##@AdobeOrg Erstanbieter-Cookie wird immer mit der Experience Cloud-Besucher-ID festgelegt.

## Verhalten von Drittanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert eine `mboxSession ID`. Die erste Ortsanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Wenn der Browser Drittanbieter-Cookies ablehnt, enthält die Weiterleitungsanfrage diese Cookies nicht und es wird überall auf der Seite Standardinhalt angezeigt. Da keine Cookies eingerichtet wurden, wird bei jeder Seitenanfrage der gleiche Prozess ausgeführt.

>[!NOTE]
>
>Das Cookie demdex.net wird gesetzt, wenn keine Third-Party-Cookies blockiert werden.

## Verhalten von Drittanbieter- und Erstanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert eine `mboxSession ID`. Die erste Ortanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Einige Browser weisen Drittanbieter-Cookies ab. Wenn das Drittanbieter-Cookie blockiert wird, funktioniert das Erstanbieter-Cookie immer noch. Target versucht, das Drittanbieter-Cookie festzulegen. Falls dies nicht möglich ist, kann Target nur die spezifische Domain des Kunden nachverfolgen. Das domänenübergreifende Tracking funktioniert nicht, wenn das Drittanbieter-Cookie blockiert wird, es sei denn, der `mboxSession` wird an den domänenübergreifenden Link angehängt. In diesem Fall wird ein weiteres Erstanbieter-Cookie gesetzt und mit dem Erstanbieter-Cookie der vorherigen Domain synchronisiert.

## Cookie-Einstellungen

Das Cookie verfügt über mehrere Standardeinstellungen. Sie können diese Einstellungen bei Bedarf ändern, mit Ausnahme der Cookie-Dauer. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie Cookie-Einstellungen ändern möchten.

| Einstellung | Informationen |
|--- |--- |
| Cookie-Name | mbox. |
| Cookie-Domäne | Die obersten und die darunter liegenden Ebenen der Domänen, von denen der Inhalt geliefert wird. Da es von der Domain Ihres Unternehmens bereitgestellt wird, handelt es sich bei dem Cookie um ein Erstanbieter-Cookie.<br />Beispiel: `mycompany.com`. |
| Serverdomäne | `clientcode.tt.omtrdc.net`, unter Verwendung des Kundencodes für Ihr Konto. |
| Cookie-Dauer | Das Cookie verbleibt zwei Wochen nach der letzten Anmeldung im Browser des Besuchers. Sie können die Cookie-Dauer nicht ändern. |
| P3P-Richtlinie | Das Cookie wird mit einer P3P-Richtlinie veröffentlicht, wie sie von den Standardeinstellungen in den meisten Browsern gefordert wird. Eine P3P-Richtlinie gibt einem Browser an, wer das Cookie bereitstellt und wie die Informationen verwendet werden. |

Das Cookie speichert verschiedene Werte, um zu verwalten, wie Ihre Besucher Kampagnen erleben:

| Wert | Definition |
|--- |--- |
| session ID | Eine eindeutige Kennung für eine Benutzersitzung. Standardmäßig dauert diese ID 30 Minuten. |
| pc ID | Eine eingeschränkt dauerhafte Kennung für den Browser eines Besuchers. Wird 14 Tage beibehalten. |
| check | Ein einfacher Testwert, mit dem bestimmt wird, ob ein Besucher Cookies unterstützt. Wird immer dann eingestellt, wenn ein Besucher eine Seite anfordert. |
| disable | Wird festgelegt, wenn die Ladezeit des Besuchers den in der JavaScript-Bibliotheksdatei konfigurierten Timeout überschreitet. Standardmäßig ist dieser Wert eine Stunde gültig. |

## Auswirkung auf Target bei Safari-Besuchern wegen der Änderungen des Trackings durch Apple WebKit

**Wie funktioniert das Adobe Target-Tracking?**

| Cookies | Details |
|--- |--- |
| Erstanbieter-Domänen | Die Standardimplementierung für Target-Kunden. Die „Mbox“-Cookies werden in der Domain des Kunden festgelegt. |
| Drittanbieter-Tracking | Das Tracking von Drittanbietern ist für Anwendungsfälle von Werbung und Targeting in Target und Adobe Audience Manager (AAM) wichtig. Für das Tracking von Drittanbietern sind Cross-Site-Scripting-Techniken erforderlich. Target verwendet zwei Cookies, „mboxSession“ und „mboxPC“, die in der Domain `clientcode.tt.omtrd.net` festgelegt sind. |

**Welchen Ansatz verfolgt Apple?**

Von Apple (übersetzter Auszug):

„Intelligent Tracking Prevention ist eine neue WebKit-Funktion, die das siteübergreifende Tracking durch die Einschränkung von Cookies und anderen Website-Daten reduziert.“

„Das nennt man siteübergreifendes Tracking und das von `example-tracker.com` verwendete Cookie wird als Drittanbieter-Cookie bezeichnet. Im Rahmen unserer Tests haben wir beliebte Webseiten gefunden, die mehr als 70 solcher Tracker verwenden, die alle insgeheim Daten der Benutzer sammeln.“

| Ansatz | Details |
|--- |--- |
| Intelligent Tracking Prevention | Weitere Informationen finden Sie unter [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) auf der Website „WebKit Open Source Web Browser Engine“. |
| Cookies | Der Umgang mit Cookies in Safari:<ul><li>Drittanbieter-Cookies, die sich nicht auf einer Domain befinden, auf die der Benutzer direkt zugreift, werden nie gespeichert. Dieses Verhalten ist nicht neu. Drittanbieter-Cookies werden in Safari bereits nicht unterstützt.</li><li>Drittanbieter-Cookies, die auf einer Domain festgelegt sind, auf die der Benutzer direkt zugreift, werden nach 24 Stunden gelöscht.</li><li>Erstanbieter-Cookies werden nach 30 Tagen gelöscht, wenn die Klassifizierung der jeweiligen Erstanbieter-Domäne zeigt, dass Benutzer siteübergreifend verfolgt werden. Dies trifft möglicherweise auf große Unternehmen zu, die Benutzer online auf verschiedene Domänen weiterleiten. Apple hat nicht klargestellt, wie genau diese Domains klassifiziert werden oder wie eine Domain bestimmen kann, ob sie als Tracking-Benutzer über mehrere Sites hinweg klassifiziert wurden.</li></ul> |
| Maschinelles Lernen zur Identifikation von siteübergreifenden Domänen | Von Apple:<br />Machine Learning Classifier: Ein maschinelles Lernmodell wird verwendet, um zu klassifizieren, welche Top-Privat-Domains den Benutzer über mehrere Sites hinweg basierend auf den erfassten Statistiken verfolgen können. Aus den zahlreichen gesammelten Statistiken haben sich drei Vektoren hervorgehoben, die einen starken Indikator für die Classification anhand aktueller Tracking-Vorgehensweisen darstellen: „Teilressource unter Anzahl der eindeutigen Domänen“, „Subframe unter Anzahl der eindeutigen Domänen“ und „Anzahl der eindeutigen Domänen weitergeleitet an“. Die gesamte Datensammlung und Classification erfolgt auf dem Gerät.<br />Wenn der Benutzer jedoch mit `example.com` als Top-Domain interagiert, die oft als Erstanbieter-Domain bezeichnet wird, betrachtet Intelligent Tracking Prevention dies als Signal, dass der Benutzer an der Website interessiert ist, und passt sein Verhalten vorübergehend an, wie in dieser Zeitleiste dargestellt:<br />Wenn der Benutzer mit `example.com` in den letzten 24 Stunden interagiert hat, sind seine Cookies verfügbar, wenn `example.com` ein Drittanbieter ist. Diese Praxis ermöglicht Anmeldeszenarien des Typs „Mit meinem X-Konto bei Y anmelden“.<ul><li>Domains, die als Domain der obersten Ebene besucht werden, sind nicht betroffen. Seiten wie beispielsweise OKTA</li><li>kennzeichnet Domains, die Subdomains oder Unterframes der aktuellen Seite über mehrere eindeutige Domains hinweg sind.</li></ul> |

**Wie ist Adobe betroffen?**

| Betroffene Funktionalität | Details |
|--- |--- |
| Abmeldeunterstützung | Wegen der durch das WebKit von Apple bewirkten Änderungen am Tracking ist die Unterstützung für Ausschlüsse hinfällig.<br />Der Target-Ausschluss verwendet ein Cookie in der `clientcode.tt.omtrdc.net`-Domain. Weitere Informationen finden Sie unter [Datenschutz](/help/dev/before-implement/privacy/privacy.md).<br />Target unterstützt zwei Arten von Ausschlüssen:<ul><li>Einen pro Kunde (der Kunde verwaltet den Ausschluss-Link).</li><li>Einen über Adobe, der den Benutzer für alle Target-Funktionalität für alle Benutzer ausschließt.</li></ul>Beide Methoden verwenden den Drittanbieter-Cookie. |
| Target-Aktivitäten | Kunden können ihre [Lebensdauer](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html?lang=de) für ihre Target-Konten auswählen (bis zu 90 Tage). Problematisch ist Folgendes: Wenn die Profillebensdauer des Kontos länger als 30 Tage ist und das Erstanbieter-Cookie gelöscht wird, da die Domain des Kunden als Tracking-Benutzer über mehrere Sites hinweg gekennzeichnet wurde, das Verhalten für Safari-Besucher in Target wie folgt beeinflusst wird:<br />**[!UICONTROL Target reports]**: Wenn ein Safari-Benutzer eine Aktivität beginnt, nach 30 Tagen zurückkehrt und dann konvertiert, zählt dieser Benutzer als zwei Besucher und eine Konversion.<br />Dieses Verhalten ist bei Aktivitäten, die Analytics verwenden, identisch mit dem Verhalten der Berichtsquelle (A4T).<br />**[!UICONTROL Profile & activity membership]**:<ul><li>Profildaten werden gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li>Die Aktivitätsmitgliedschaft wird gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li> Target funktioniert in Safari nicht bei Konten, die eine Implementation mit Drittanbieter-Cookie oder Erst- und Drittanbieter-Cookie verwenden. Dieses Verhalten ist nicht neu. Safari lässt Cookies von Drittanbietern schon eine Weile nicht mehr zu.</li></ul><br />**[!UICONTROL Suggestions]**: Wenn Sie befürchten, dass die Domain des Kunden möglicherweise als Domain markiert wird, die Besucher sitzungsübergreifend verfolgt, ist es am sichersten, die Profillebensdauer in Target auf 30 Tage oder weniger festzulegen. Diese Begrenzung stellt sicher, dass Benutzer in Safari und allen anderen Browsern ähnlich verfolgt werden. |
