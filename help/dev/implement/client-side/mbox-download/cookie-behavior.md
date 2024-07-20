---
keywords: Übersicht und Referenz, Webkit, Cookies, Erstanbieter, Drittanbieter, Erstanbieter, Drittanbieter, 8 USD
description: Erfahren Sie mehr über das Verhalten von Target-Cookies (Erstanbieter-Cookie, Drittanbieter-Cookie mit Erstanbieter-Cookie oder Drittanbieter-Cookie allein).
title: Wo finde ich Informationen über Target-Cookies?
feature: at.js
role: Developer
source-git-commit: 34e8625798121e236a04646dfcf049f9c2b6f9d0
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 53%

---

# Cookies in Target

Das Verhalten von Cookies ist davon abhängig, ob es sich um ein Erstanbieter-Cookie, ein Drittanbieter-Cookie mit Erstanbieter-Cookie oder nur um ein Drittanbieter-Cookie handelt.

>[!NOTE]
>
>Dieses Thema enthält Informationen zu `mboxSession` und `mboxPC`. Best Practices bei der Implementierung empfehlen, vertrauliche Informationen nicht mit den Cookie-Daten zu verknüpfen oder zu speichern: `mboxSession` oder `mboxPC`.

Siehe auch [Löschen des Target-Cookies](/help/dev/before-implement/privacy/cookie-deleting.md).

## Verwenden von Erstanbieter-Cookies und Drittanbieter-Cookies

Durch Ihre Site-Einrichtung wird bestimmt, welche Cookies Sie verwenden. Um Erstanbieter- und Drittanbieter-Cookies zu verstehen, ist es hilfreich, die Funktionsweise von Target zu verstehen. Weitere Informationen finden Sie unter [Funktionsweise von Adobe Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) .

Es gibt drei Haupt-Nutzungsszenarien für Cookies:

1. Eine Domain.

   Alle Tests finden innerhalb einer Domäne der obersten Ebene (`www.domain.com`, `store.domain.com`, `anysub.domain.com` usw.) statt.

   Ansatz: Verwenden Sie nur Erstanbieter-Cookies (Standard).

1. Die Benutzer wechseln zwischen Domänen und Sie möchten ihr Verhalten auf allen diesen Domänen nachverfolgen und testen.

   Beispiel: Ein Benutzer besucht Ihren Onlineshop, geht aber über Yahoo Store zum Checkout. Drei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer die beste Vorgehensweise):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.
   * Nur Drittanbieter-Cookies aktivieren (selten, doch der Vorteil ist, dass das Mbox-Cookie von Ihrer Domäne fern bleibt).
   * Nur Erstanbieter-Cookies aktivieren und den Parameter `mboxSession` beim Wechseln von Domänen weitergeben.

     Der Parameter `mboxSession` muss an eine Landingpage übergeben und aus der JavaScript-Bibliothek (Adobe Experience Platform Web SDK oder at.js) referenziert werden. Es darf sich nicht um eine Zwischenseite als Weiterleitung handeln.

1. Sie verwenden nur AdBoxes oder Flashboxes auf einer Site eines Drittanbieters.

   Zwei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer den besten Ansatz):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.

     Erstanbieter- und Drittanbieter-Cookies sind für Flashbox- und dynamische Kreativinhalte erforderlich.

   * Nur Drittanbieter-Cookies aktivieren.

     Diese Vorgehensweise wird nur in seltenen Fällen angewendet, in denen AdBox-Implementierungen ohne On-Site-Targeting verwendet werden.

## Verhalten von Erstanbieter-Cookies

Das Erstanbieter-Cookie wird unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domäne ist.

Die JavaScript-Bibliothek generiert einen `mboxSession ID` und speichert ihn im Target-Cookie. Die erste Mbox-Antwort enthält das Angebot und die JavaScript, um die von der Anwendung erzeugte `mboxPC ID` im Mbox-Cookie zu speichern.

>[!NOTE]
>
>Das Erstanbieter-Cookie AMCV_##@AdobeOrg wird immer mit der Experience Cloud-Besucher-ID festgelegt.

## Verhalten von Drittanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domäne ist.

Die JavaScript-Bibliothek generiert eine &quot;`mboxSession ID`&quot;. Die erste Ortsanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Wenn der Browser Drittanbieter-Cookies ablehnt, enthält die Weiterleitungsanfrage diese Cookies nicht und es wird überall auf der Seite Standardinhalt angezeigt. Da keine Cookies eingerichtet wurden, wird bei jeder Seitenanfrage der gleiche Prozess ausgeführt.

>[!NOTE]
>
>Das Cookie demdex.net wird gesetzt, wenn Drittanbieter-Cookies nicht blockiert werden.

## Verhalten von Drittanbieter- und Erstanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domäne ist.

Die JavaScript-Bibliothek generiert eine &quot;`mboxSession ID`&quot;. Die erste Ortanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Einige Browser weisen Drittanbieter-Cookies ab. Wenn das Drittanbieter-Cookie blockiert wird, funktioniert das Erstanbieter-Cookie immer noch. Target versucht, das Drittanbieter-Cookie festzulegen. Falls dies nicht möglich ist, kann Target nur die spezifische Domäne des Kunden nachverfolgen. Das domänenübergreifende Tracking funktioniert nicht, wenn das Drittanbieter-Cookie blockiert ist, es sei denn, der `mboxSession` ist an den domänenüberschreitenden Link angehängt. In diesem Fall wird ein weiteres Erstanbieter-Cookie gesetzt und mit dem Erstanbieter-Cookie der vorherigen Domain synchronisiert.

## Cookie-Einstellungen

Das Cookie verfügt über mehrere Standardeinstellungen. Sie können diese Einstellungen bei Bedarf ändern, mit Ausnahme der Cookie-Dauer. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie Cookie-Einstellungen ändern möchten.

| Einstellung | Informationen |
|--- |--- |
| Cookie-Name | mbox. |
| Cookie-Domäne | Die obersten und die darunter liegenden Ebenen der Domänen, von denen der Inhalt geliefert wird. Da der Cookie von der Domäne Ihres Unternehmens bereitgestellt wird, handelt es sich um ein Erstanbieter-Cookie.<br />Beispiel: `mycompany.com`. |
| Serverdomäne | `clientcode.tt.omtrdc.net`, unter Verwendung des Kundencodes für Ihr Konto. |
| Cookie-Dauer | Das Cookie verbleibt zwei Wochen nach der letzten Anmeldung im Browser des Besuchers. Sie können die Cookie-Dauer nicht ändern. |
| P3P-Richtlinie | Das Cookie wird mit einer P3P-Richtlinie veröffentlicht, wie sie von den Standardeinstellungen in den meisten Browsern gefordert wird. Eine P3P-Richtlinie gibt einem Browser an, wer das Cookie bereitstellt und wie die Informationen verwendet werden. |

Das Cookie enthält verschiedene Werte, um zu verwalten, wie Ihre Besucher Kampagnen erleben:

| Wert | Definition |
|--- |--- |
| session ID | Eine eindeutige Kennung für eine Benutzersitzung. Standardmäßig ist diese ID 30 Minuten gültig. |
| pc ID | Eine eingeschränkt dauerhafte Kennung für den Browser eines Besuchers. Wird 14 Tage beibehalten. |
| check | Ein einfacher Testwert, mit dem bestimmt wird, ob ein Besucher Cookies unterstützt. Wird immer dann eingestellt, wenn ein Besucher eine Seite anfordert. |
| disable | Wird eingestellt, wenn die Ladezeit des Besuchers die in der JavaScript-Bibliotheksdatei konfigurierte Zeitüberschreitung überschreitet. Standardmäßig ist dieser Wert eine Stunde gültig. |

## Auswirkung auf Target bei Safari-Besuchern wegen der Änderungen des Trackings durch Apple WebKit

**Wie funktioniert das Adobe Target-Tracking?**

| Cookies | Details |
|--- |--- |
| Erstanbieter-Domänen | Die standardmäßige Implementierung für Target-Kunden. Die „Mbox“-Cookies werden in der Domain des Kunden festgelegt. |
| Drittanbieter-Tracking | Das Tracking von Drittanbietern ist für Anwendungsfälle für Werbung und Targeting in Target und in Adobe Audience Manager (AAM) wichtig. Für das Drittanbieter-Tracking sind Site-übergreifende Skriptmethoden erforderlich. Target verwendet zwei Cookies, „mboxSession“ und „mboxPC“, die in der Domain `clientcode.tt.omtrd.net` festgelegt sind. |
**Welchen Ansatz verfolgt Apple?**

Von Apple (übersetzter Auszug):

„Intelligent Tracking Prevention ist eine neue WebKit-Funktion, die das siteübergreifende Tracking durch die Einschränkung von Cookies und anderen Website-Daten reduziert.“

„Das nennt man siteübergreifendes Tracking und das von `example-tracker.com` verwendete Cookie wird als Drittanbieter-Cookie bezeichnet. Im Rahmen unserer Tests haben wir beliebte Webseiten gefunden, die mehr als 70 solcher Tracker verwenden, die alle insgeheim Daten der Benutzer sammeln.“

| Ansatz | Details |
|--- |--- |
| Intelligent Tracking Prevention | Weitere Informationen finden Sie unter [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) auf der Website „WebKit Open Source Web Browser Engine“. |
| Cookies | Der Umgang mit Cookies in Safari:<ul><li>Drittanbieter-Cookies, die sich nicht auf einer Domain befinden, auf die der Benutzer direkt zugreift, werden nie gespeichert. Dieses Verhalten ist nicht neu. Drittanbieter-Cookies werden in Safari bereits nicht unterstützt.</li><li>Drittanbieter-Cookies, die auf einer Domain festgelegt sind, auf die der Benutzer direkt zugreift, werden nach 24 Stunden gelöscht.</li><li>Erstanbieter-Cookies werden nach 30 Tagen gelöscht, wenn die Klassifizierung der jeweiligen Erstanbieter-Domäne zeigt, dass Benutzer siteübergreifend verfolgt werden. Dies trifft möglicherweise auf große Unternehmen zu, die Benutzer online auf verschiedene Domänen weiterleiten. Apple hat nicht klargestellt, wie genau diese Domänen klassifiziert sind oder wie eine Domäne feststellen kann, ob sie als seitenübergreifendes Tracking von Benutzern klassifiziert wurden.</li></ul> |
| Maschinelles Lernen zur Identifikation von siteübergreifenden Domänen | Von Apple:<br />Machine Learning Classifier: Ein Modell für maschinelles Lernen wird verwendet, um zu klassifizieren, welche privat registrierten Top-Level-Domains den Benutzer anhand der erfassten Statistiken siteübergreifend verfolgen können. Aus den zahlreichen gesammelten Statistiken haben sich drei Vektoren hervorgehoben, die einen starken Indikator für die Classification anhand aktueller Tracking-Vorgehensweisen darstellen: „Teilressource unter Anzahl der eindeutigen Domänen“, „Subframe unter Anzahl der eindeutigen Domänen“ und „Anzahl der eindeutigen Domänen weitergeleitet an“. Die gesamte Datensammlung und Classification erfolgt auf dem Gerät.<br />Wenn der Benutzer jedoch mit `example.com` als oberster Domäne interagiert, die häufig als Erstanbieterdomäne bezeichnet wird, betrachtet Intelligent Tracking Prevention dies als Signal, dass der Benutzer an der Website interessiert ist, und passt sein Verhalten vorübergehend an, wie in dieser Zeitleiste dargestellt:<br />Wenn der Benutzer in den letzten 24 Stunden mit `example.com` interagiert hat, sind seine Cookies verfügbar, wenn `example.com` ein Drittanbieter ist. Diese Vorgehensweise ermöglicht Anmeldeszenarien mit &quot;Mit meinem X-Konto bei Y anmelden&quot;.<ul><li>Domänen, die als Domäne der obersten Ebene besucht werden, sind nicht betroffen. Seiten wie beispielsweise OKTA</li><li>Identifiziert Domänen, die Unterdomäne oder Unterframe der aktuellen Seite sind, domänenübergreifend.</li></ul> |

**Wie wirkt sich Adobe aus?**

| Betroffene Funktionalität | Details |
|--- |--- |
| Abmeldeunterstützung | Wegen der durch das WebKit von Apple bewirkten Änderungen am Tracking ist die Unterstützung für Ausschlüsse hinfällig.<br />Der Target-Ausschluss verwendet ein Cookie in der `clientcode.tt.omtrdc.net`-Domain. Weitere Informationen finden Sie unter [Datenschutz](/help/dev/before-implement/privacy/privacy.md).<br />Target unterstützt zwei Arten von Ausschlüssen:<ul><li>Einen pro Kunde (der Kunde verwaltet den Ausschluss-Link).</li><li>Einen über Adobe, der den Benutzer für alle Target-Funktionalität für alle Benutzer ausschließt.</li></ul>Beide Methoden verwenden den Drittanbieter-Cookie. |
| Target-Aktivitäten | Kunden können für ihre Target-Konten ihre [Lebensdauer des Profils](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) auswählen (bis zu 90 Tage). Wenn die Profillebensdauer des Kontos länger als 30 Tage ist und das Erstanbieter-Cookie gelöscht wird, weil die Domäne des Kunden als Site-übergreifendes Tracking von Benutzern markiert wurde, wirkt sich das Verhalten von Safari-Besuchern in Target auf die folgenden Bereiche aus:<br />**[!UICONTROL Target reports]**: Wenn ein Safari-Benutzer eine Aktivität aufnimmt, nach 30 Tagen zurückkehrt und dann konvertiert, zählt dieser Benutzer als zwei Besucher und eine Konversion.<br />Dieses Verhalten ist bei Aktivitäten mit Analytics als Berichtsquelle (A4T) identisch.<br />**[!UICONTROL Profile & activity membership]**:<ul><li>Profildaten werden gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li>Die Aktivitätsmitgliedschaft wird gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li> Target funktioniert in Safari nicht bei Konten, die eine Implementation mit Drittanbieter-Cookie oder Erst- und Drittanbieter-Cookie verwenden. Dieses Verhalten ist nicht neu. Safari hat für eine Weile keine Drittanbieter-Cookies zugelassen.</li></ul><br />**[!UICONTROL Suggestions]**: Wenn Bedenken bestehen, dass die Kundendomäne möglicherweise als eine Domäne markiert wird, die Besucher sitzungsübergreifend verfolgt, ist es am sichersten, die Profillebensdauer in Target auf 30 Tage oder weniger festzulegen. Mit dieser Beschränkung wird sichergestellt, dass Benutzer in Safari und allen anderen Browsern auf ähnliche Weise verfolgt werden. |
