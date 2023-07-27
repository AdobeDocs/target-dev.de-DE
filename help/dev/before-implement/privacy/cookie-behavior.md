---
keywords: Übersicht und Referenz, Webkit, Cookies, Erstanbieter, Drittanbieter, Erstanbieter, Drittanbieter,
description: Informationen zu [!DNL Target] Cookie-Verhalten (Erstanbieter-Cookie, Drittanbieter-Cookie mit Erstanbieter-Cookie oder nur Drittanbieter-Cookie).
title: Wo finde ich Informationen? [!DNL Target] Cookies?
feature: at.js
exl-id: d44e02ce-8920-4130-bcad-699ca77c0dad
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 57%

---

# [!DNL Target] Cookies

Das Verhalten von Cookies ist davon abhängig, ob es sich um ein Erstanbieter-Cookie, ein Drittanbieter-Cookie mit Erstanbieter-Cookie oder nur um ein Drittanbieter-Cookie handelt.

>[!NOTE]
>
>Detaillierte Informationen zu den verschiedenen Cookies, die von [!DNL Target], siehe [[!DNL Adobe Target] Cookies](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-target.html?lang=de){target=_blank} im *Komponentenleitfaden für die zentrale Benutzeroberfläche von Experience Cloud*.
>
>Dieses Thema enthält Informationen zu `mboxSession` und `mboxPC`. Best Practices bei der Implementierung empfehlen, vertrauliche Informationen nicht mit den Cookie-Daten zu verknüpfen oder zu speichern: `mboxSession` oder `mboxPC`.

Siehe auch [Löschen Sie die [!DNL Target] Cookie](cookie-deleting.md).

## Verwendung von Erstanbieter- oder Drittanbieter-Cookies

Durch Ihre Site-Einrichtung wird bestimmt, welche Cookies Sie verwenden. Es ist hilfreich zu verstehen, wie [!DNL Target] funktioniert beim Versuch, Erstanbieter- und Drittanbieter-Cookies zu verstehen. Siehe [ [!DNL Adobe] [!DNL Target]Funktionsweise von ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html) für weitere Informationen.

Es gibt drei Haupt-Nutzungsszenarien für Cookies:

1. Eine Domain.

   Alle Tests finden innerhalb einer Top-Level-Domäne (`www.domain.com`, `store.domain.com`, `anysub.domain.com`usw.).

   Ansatz: Verwenden Sie nur Erstanbieter-Cookies (Standard).

1. Die Benutzer wechseln zwischen Domänen und Sie möchten ihr Verhalten auf allen diesen Domänen nachverfolgen und testen.

   Beispiel: Ein Benutzer besucht Ihren Onlineshop, geht aber über Yahoo Store zum Checkout. Drei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer die beste Vorgehensweise):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.
   * Nur Drittanbieter-Cookies aktivieren (selten, doch der Vorteil ist, dass das Mbox-Cookie von Ihrer Domäne fern bleibt).
   * Nur Erstanbieter-Cookies aktivieren und den Parameter `mboxSession` beim Wechseln von Domänen weitergeben.

     Die `mboxSession` -Parameter müssen an eine Landingpage weitergegeben und aus der JavaScript-Bibliothek (Adobe Experience Platform Web SDK oder at.js) referenziert werden. Es darf sich nicht um eine Zwischenseite als Weiterleitung handeln.

1. Sie verwenden nur AdBoxes oder Flashboxes auf einer Site eines Drittanbieters.

   Zwei Vorgehensweisen (erarbeiten Sie mit Ihrem Kundenbetreuer den besten Ansatz):

   * Erstanbieter- und Drittanbieter-Cookies aktivieren.

     Erstanbieter- und Drittanbieter-Cookies sind für Flashbox- und dynamische Kreativinhalte erforderlich.

   * Nur Drittanbieter-Cookies aktivieren.

     Diese Vorgehensweise wird nur in seltenen Fällen angewendet, in denen AdBox-Implementierungen ohne On-Site-Targeting verwendet werden.

## Verhalten von Erstanbieter-Cookies

Das Erstanbieter-Cookie wird unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert eine `mboxSession ID` und speichert sie im [!DNL Target] Cookie. Die erste Mbox-Antwort enthält das Angebot und das JavaScript zum Speichern der `mboxPC ID` von der Anwendung generiert wurde, im Mbox-Cookie.

>[!NOTE]
>
>Das Erstanbieter-Cookie AMCV_##@AdobeOrg wird immer mit der Experience Cloud-Besucher-ID festgelegt.

## Verhalten von Drittanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert eine `mboxSession ID`. Die erste Ortsanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Wenn der Browser Drittanbieter-Cookies ablehnt, enthält die Weiterleitungsanfrage diese Cookies nicht und es wird überall auf der Seite Standardinhalt angezeigt. Da keine Cookies eingerichtet wurden, wird bei jeder Seitenanfrage der gleiche Prozess ausgeführt.

>[!NOTE]
>
>Wenn Cookies von Drittanbietern nicht blockiert werden, wird das Cookie demdex.net gesetzt.

## Verhalten von Drittanbieter- und Erstanbieter-Cookies

Das Drittanbieter-Cookie wird unter clientcode.tt.omtrdc.net und das Erstanbieter-Cookie unter clientdomain.com gespeichert, wobei `clientdomain` Ihre Domain ist.

Die JavaScript-Bibliothek generiert eine `mboxSession ID`. Die erste Ortanforderung gibt HTTP-Antwortheader zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet.

Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Angebot wird zurückgegeben.

Einige Browser weisen Drittanbieter-Cookies ab. Wenn das Drittanbieter-Cookie blockiert wird, funktioniert das Erstanbieter-Cookie immer noch. [!DNL Target] versucht, das Drittanbieter-Cookie festzulegen. Falls dies nicht möglich ist, kann [!DNL Target] nur die spezifische Domain des Kunden nachverfolgen. Domänenübergreifendes Tracking funktioniert nicht, wenn das Drittanbieter-Cookie blockiert ist, es sei denn, die `mboxSession` an den domänenüberschreitenden Link angehängt. In diesem Fall wird ein weiteres Erstanbieter-Cookie gesetzt und mit dem Erstanbieter-Cookie der vorherigen Domain synchronisiert.

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
| disable | Wird eingestellt, wenn die Ladezeit des Besuchers den in der JavaScript-Bibliotheksdatei konfigurierten Timeout überschreitet. Standardmäßig ist dieser Wert eine Stunde gültig. |

## Auswirkungen auf [!DNL Target] für Safari-Besucher aufgrund von Tracking-Änderungen in Apple WebKit

**Wie funktioniert [!DNL Target] Tracking-Arbeit?**

| Cookies | Details |
|--- |--- |
| Erstanbieter-Domänen | Die Standardimplementierung für [!DNL Target] -Kunden. Die „Mbox“-Cookies werden in der Domain des Kunden festgelegt. |
| Drittanbieter-Tracking | Das Tracking von Drittanbietern ist für Anwendungsfälle von Werbung und Targeting in [!DNL Target] und [!DNL Adobe Audience Manager] AAM. Für das Drittanbieter-Tracking sind siteübergreifende Techniken zur Skripterstellung erforderlich. [!DNL Target] verwendet zwei Cookies, „mboxSession“ und „mboxPC“, die in der Domain `clientcode.tt.omtrd.net` festgelegt sind. |
**Welchen Ansatz verfolgt Apple?**

Von Apple (übersetzter Auszug):

„Intelligent Tracking Prevention ist eine neue WebKit-Funktion, die das siteübergreifende Tracking durch die Einschränkung von Cookies und anderen Website-Daten reduziert.“

„Das nennt man siteübergreifendes Tracking und das von `example-tracker.com` verwendete Cookie wird als Drittanbieter-Cookie bezeichnet. Im Rahmen unserer Tests haben wir beliebte Webseiten gefunden, die mehr als 70 solcher Tracker verwenden, die alle insgeheim Daten der Benutzer sammeln.“

| Ansatz | Details |
|--- |--- |
| Intelligent Tracking Prevention | Weitere Informationen finden Sie unter [Intelligent Tracking Prevention](https://webkit.org/blog/7675/intelligent-tracking-prevention/) auf der Website „WebKit Open Source Web Browser Engine“. |
| Cookies | Der Umgang mit Cookies in Safari:<ul><li>Drittanbieter-Cookies, die sich nicht auf einer Domain befinden, auf die der Benutzer direkt zugreift, werden nie gespeichert. Dieses Verhalten ist nicht neu. Drittanbieter-Cookies werden in Safari bereits nicht unterstützt.</li><li>Drittanbieter-Cookies, die auf einer Domain festgelegt sind, auf die der Benutzer direkt zugreift, werden nach 24 Stunden gelöscht.</li><li>Erstanbieter-Cookies werden nach 30 Tagen gelöscht, wenn die Klassifizierung der jeweiligen Erstanbieter-Domäne zeigt, dass Benutzer siteübergreifend verfolgt werden. Dies trifft möglicherweise auf große Unternehmen zu, die Benutzer online auf verschiedene Domänen weiterleiten. Apple hat nicht klargestellt, wie genau diese Domänen klassifiziert sind oder wie eine Domäne feststellen kann, ob sie als seitenübergreifendes Tracking von Benutzern klassifiziert wurden.</li></ul> |
| Maschinelles Lernen zur Identifikation von siteübergreifenden Domänen | Von Apple (übersetzter Auszug):<br />Machine Learning Classifier: Basierend auf den erfassten Statistiken wird anhand eines maschinell lernenden Modells klassifiziert, welche privat registrierten Top-Level-Domains den Benutzer siteübergreifend verfolgen können. Aus den zahlreichen gesammelten Statistiken haben sich drei Vektoren hervorgehoben, die einen starken Indikator für die Classification anhand aktueller Tracking-Vorgehensweisen darstellen: „Teilressource unter Anzahl der eindeutigen Domänen“, „Subframe unter Anzahl der eindeutigen Domänen“ und „Anzahl der eindeutigen Domänen weitergeleitet an“. Die gesamte Datensammlung und Classification erfolgt auf dem Gerät.<br />Wenn der Benutzer jedoch mit `example.com` als oberste Domäne, häufig als Erstanbieterdomäne bezeichnet, betrachtet Intelligent Tracking Prevention dies als Signal, dass der Benutzer an der Website interessiert ist, und passt sein Verhalten vorübergehend an, wie in dieser Zeitleiste dargestellt:<br />Wenn der Benutzer mit `example.com` In den letzten 24 Stunden sind die Cookies verfügbar, wenn `example.com` ist ein Drittanbieter. Diese Vorgehensweise ermöglicht Anmeldeszenarien mit &quot;Mit meinem X-Konto bei Y anmelden&quot;.<ul><li>Domänen, die als Domäne der obersten Ebene besucht werden, sind nicht betroffen. Seiten wie beispielsweise OKTA</li><li>Domänen, bei denen es sich um Sub-Domänen oder Subframes der aktuellen Seite handelt, werden über mehrere eindeutige Domänen hinweg identifiziert.</li></ul> |

**Wie ist [!DNL Adobe] Betroffen?**

| Betroffene Funktionalität | Details |
|--- |--- |
| Abmeldeunterstützung | Wegen der durch das WebKit von Apple bewirkten Änderungen am Tracking ist die Unterstützung für Ausschlüsse hinfällig.<br />Der Target-Ausschluss verwendet ein Cookie in der `clientcode.tt.omtrdc.net`-Domain. Weitere Informationen finden Sie unter [Datenschutz](privacy.md).<br />Target unterstützt zwei Arten von Ausschlüssen:<ul><li>Einen pro Kunde (der Kunde verwaltet den Ausschluss-Link).</li><li>Eins über [!DNL Adobe] , die den Benutzer von allen [!DNL Target] für alle Kunden.</li></ul>Beide Methoden verwenden den Drittanbieter-Cookie. |
| Target-Aktivitäten | Kunden können die  [Profillebensdauer](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) für ihre [!DNL Target] Konten (bis zu 90 Tage). Wenn die Profillebensdauer des Kontos länger als 30 Tage ist und das Erstanbieter-Cookie gelöscht wird, weil die Domäne des Kunden als Site-übergreifendes Tracking von Benutzern markiert wurde, besteht das Problem darin, dass das Verhalten von Safari-Besuchern in den folgenden Bereichen in Target beeinträchtigt wird:<br />**Zielberichte**: Wenn ein Safari-Benutzer eine Aktivität aufruft, nach 30 Tagen zurückkehrt und dann konvertiert, zählt dieser Benutzer als zwei Besucher und eine Konversion.<br />Dieses Verhalten gilt auch für Aktivitäten, die Analytics als Berichtsquelle nutzen (A4T).<br />**Profil- und Aktivitätsmitgliedschaft**:<ul><li>Profildaten werden gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li>Die Aktivitätsmitgliedschaft wird gelöscht, wenn das Erstanbieter-Cookie abläuft.</li><li> [!DNL Target] funktioniert in Safari nicht bei Konten, die eine Implementation mit Drittanbieter-Cookie oder Erst- und Drittanbieter-Cookie verwenden. Dieses Verhalten ist nicht neu. Safari hat für eine Weile keine Drittanbieter-Cookies zugelassen.</li></ul><br />**Empfehlungen**: Wenn Sie befürchten, dass die Kundendomäne als eine Domäne markiert wird, die Besucher sitzungsübergreifend verfolgt, ist es am sichersten, die Profillebensdauer in Target auf 30 Tage oder weniger festzulegen. Mit dieser Beschränkung wird sichergestellt, dass Benutzer in Safari und allen anderen Browsern auf ähnliche Weise verfolgt werden. |
