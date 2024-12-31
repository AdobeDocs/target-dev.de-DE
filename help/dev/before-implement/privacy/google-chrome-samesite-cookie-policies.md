---
keywords: Google, SameSite, Cookies, Chrome 80, IETF
description: Erfahren Sie [!DNL Adobe Target]  wie der SameSite-IETF-Standard gehandhabt wird, der mit Google Chrome Version 80 eingeführt wird, und was Sie tun müssen, um diese Richtlinien zu erfüllen.
title: Wie handhabt  [!DNL Target]  die SameSite-Cookie-Richtlinien von Google?
feature: Privacy & Security
exl-id: 58a83def-9625-4d44-914f-203509c6c434
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 68%

---

# SameSite-Cookie-Richtlinien von Google Chrome

Google implementierte mit der Release von Chrome 80 Anfang 2020 neue Cookie-Richtlinien für Benutzer. In diesem Artikel erfahren Sie alles, was Sie über die neuen SameSite-Cookie-Richtlinien wissen müssen, wie [!DNL Adobe Target] diese Richtlinien unterstützt und wie Sie [!DNL Target] verwenden können, um die neuen SameSite-Cookie-Richtlinien von Google Chrome einzuhalten.

Ab Chrome 80 müssen Web-Entwickler explizit angeben, welche Cookies Website-übergreifend genutzt werden. Dies ist die erste von vielen Ankündigungen, die Google zur Verbesserung des Datenschutzes und der Sicherheit im Internet plant.

In Anbetracht der Tatsache, dass Facebook in Bezug auf Datenschutz und Sicherheit in der Kritik steht, haben andere große Unternehmen wie Apple und jetzt auch Google die Gelegenheit genutzt, um sich in der neuen Rolle als Verfechter des Datenschutzes und der Sicherheit zu beweisen. Apple war das erste Unternehmen, das aktiv wurde, und kündigte Anfang des Jahres mit ITP 2.1 und kürzlich mit ITP 2.2 Änderungen an seinen Cookie-Richtlinien an. Mit ITP 2.1 blockiert Apple Cookies von Drittanbietern vollständig und speichert Cookies, die im Browser erstellt werden, nur sieben Tage lang. Mit ITP 2.2 werden Cookies nur einen Tag lang aufbewahrt. Googles Ankündigung ist bei weitem nicht so aggressiv wie die Apples, aber sie ist der erste Schritt in Richtung desselben Ziels. Weitere Informationen zu den Apple-Richtlinien finden Sie unter [Apple Intelligent Tracking Prevention (ITP) 2.x](/help/dev/before-implement/privacy/apple-itp-2x.md).

## Was sind Cookies und wie werden sie verwendet?

Bevor wir uns mit den Änderungen der Cookie-Richtlinien von Google befassen, sollten wir uns damit befassen, was Cookies sind und wie sie verwendet werden. Einfach ausgedrückt, sind Cookies kleine Textdateien, die im Webbrowser gespeichert und zum Erfassen von Benutzerattributen verwendet werden.

Cookies sind wichtig, da sie das Benutzererlebnis beim Surfen im Internet verbessern. Wenn Sie z. B. auf einer E-Commerce-Website einkaufen und etwas in Ihren Warenkorb legen, sich aber bei diesem Besuch nicht anmelden oder einkaufen, speichern Cookies Ihre Artikel und behalten sie für Ihren nächsten Besuch in Ihrem Warenkorb. Stellen Sie sich vor, Sie wären gezwungen, bei jedem Besuch einer häufig von Ihnen genutzten Social-Media-Website Ihren Benutzernamen und Ihr Passwort erneut einzugeben. Cookies lösen auch dieses Problem, da sie Informationen speichern, die den Websites dabei helfen, Ihre Identität festzustellen. Diese Arten von Cookies werden als Erstanbieter-Cookies bezeichnet, da sie von der von Ihnen besuchten Website erstellt und verwendet werden.

Es gibt auch Drittanbieter-Cookies. Sehen wir uns folgendes Beispiel an, um sie besser zu verstehen:

Nehmen wir an, ein imaginäres Social-Media-Unternehmen namens „Friends“ stellt eine Freigabe-Schaltfläche bereit, die von anderen Sites implementiert werden kann, damit die Friends-Benutzer die Inhalte der Website im Feed der Friends-Website teilen können. Ein Benutzer liest einen Nachrichtenartikel auf einer Nachrichten-Website, die die Freigabe-Schaltfläche verwendet, und klickt darauf, um ihn automatisch in seinem Friends-Konto zu posten.

Damit das möglich ist, ruft der Browser beim Laden des Nachrichtenartikels die Freigabe-Schaltfläche der Friends-Website von `platform.friends.com` ab. Im Zuge dieses Prozesses hängt der Browser Friends-Cookies, die die Anmeldedaten des Benutzers enthalten, an die Anfrage an die Friends-Server an. Auf diese Weise können Friends den Nachrichtenartikel in seinem Feed im Namen des Benutzers posten, ohne dass sich der Benutzer anmelden muss.

Dies ist alles durch die Verwendung von Drittanbieter-Cookies möglich. In diesem Fall wird das Drittanbieter-Cookie im Browser zur `platform.friends.com` gespeichert, sodass `platform.friends.com` das Posting in der Friends-App im Namen des Benutzers ausführen können.

Wenn Sie sich einen Moment vorstellen, wie dieses Szenario ohne Drittanbieter-Cookies aussehen würde, müsste der Benutzer viele manuelle Schritte ausführen. Zunächst müsste der Benutzer den Link zum Nachrichtenartikel kopieren. Dann müsste sich der Benutzer bei der Friends-App anmelden. Anschließend müsste der Benutzer auf die Schaltfläche „Beitrag erstellen“ klicken. Danach müsste der Benutzer den Link in das Textfeld kopieren und abschließend auf „Posten“ klicken. Wie Sie sehen, verbessern Drittanbieter-Cookies die Benutzerfreundlichkeit erheblich, da die manuellen Schritte drastisch reduziert werden können.

Im Allgemeinen ermöglichen Drittanbieter-Cookies die Speicherung von Daten im Browser eines Benutzers, ohne dass dieser eine Website besuchen muss.

## Sicherheitsbedenken

Obwohl Cookies Benutzererlebnisse verbessern und die Schaltung von Werbeanzeigen optimieren, können sie auch Sicherheitslücken enthalten, die CSRF-Angriffe (Cross Site Request Forgery) ermöglichen. Wenn sich ein Benutzer beispielsweise auf einer Bank-Website anmeldet, um Kreditkartenrechnungen zu bezahlen, und die Website verlässt, ohne sich abzumelden, und dann in derselben Sitzung zu einer böswilligen Site navigiert, kann es zu einem CSRF-Angriff kommen. Die böswillige Site kann Code enthalten. Dieser kann eine Anfrage an die Bank-Site senden und wenn die Seite geladen wird, kann diese Anfrage ausgeführt werden. Da der Benutzer weiterhin auf der Bank-Site authentifiziert ist, kann das Sitzungs-Cookie verwendet werden, um einen CSRF-Angriff durchzuführen und ein Überweisungsereignis aus dem Bankkonto des Benutzers zu initiieren. Dies liegt daran, dass bei jedem Besuch einer Site alle Cookies in der HTTP-Anfrage angehängt werden. Und aufgrund dieser Sicherheitsbedenken versucht Google jetzt, diese Schwachstelle zu beheben.

## Wie verwendet [!DNL Target] Cookies?

Sehen wir uns einmal an, wie [!DNL Target] Cookies verwendet. Damit Sie [!DNL Target] überhaupt verwenden können, müssen Sie die [!DNL Target] JavaScript-Bibliothek auf Ihrer Site installieren. Dadurch können Sie ein Erstanbieter-Cookie im Browser des Benutzers platzieren, der Ihre Site besucht. Während der Benutzer mit Ihrer Website interagiert, können Sie die Verhaltens- und Interessensdaten des Benutzers über die JavaScript-Bibliothek an [!DNL Target] weitergeben. Die [!DNL Target] JavaScript-Bibliothek verwendet Erstanbieter-Cookies, um Identifizierungsinformationen über den Benutzer zu extrahieren und diese den Verhaltens- und Interessensdaten des Benutzers zuzuordnen. Diese Daten werden dann von [!DNL Target] für Ihre Personalisierungsaktivitäten verwendet.

Target verwendet auch (manchmal) Drittanbieter-Cookies. Wenn Sie über mehrere Websites verfügen, die sich auf unterschiedlichen Domains befinden, und die Journey eines Benutzers auf diesen Websites verfolgen möchten, können Sie Drittanbieter-Cookies verwenden, indem Sie Domain-übergreifendes Tracking nutzen. Wenn Sie Domain-übergreifendes Tracking in der [!DNL Target] JavaScript-Bibliothek aktivieren, verwendet Ihr Konto Drittanbieter-Cookies. Wenn ein Benutzer von einer Domain zu einer anderen wechselt, kommuniziert der Browser mit dem Backend-Server von Target, wodurch ein Drittanbieter-Cookie erstellt und im Browser des Benutzers platziert wird. Durch das Drittanbieter-Cookie im Browser des Benutzers ist [!DNL Target] in der Lage, einem einzelnen Benutzer ein konsistentes Erlebnis über verschiedene Domains hinweg bereitzustellen.

## Googles neues Cookie-Rezept

Um die Sicherheit der Benutzer zu verbessern, wenn Cookies über Sites hinweg gesendet werden, plant Google, einen IETF-Standard namens SameSite zu unterstützen. Im Rahmen dieses Standards müssen Web-Entwickler Cookies mit dem SameSite-Attribut in der Set-Cookie-Kopfzeile versehen.

Es gibt drei verschiedene Werte, die an das Attribut SameSite übergeben werden können: „Streng“, „Nicht streng“ und „Keine“.

| Wert | Beschreibung |
| --- | --- |
| Streng | Auf Cookies mit dieser Einstellung kann nur zugegriffen werden, wenn die Domain besucht wird, auf der der Cookie eingerichtet wurde. Mit anderen Worten: die Einstellung „Streng“ verhindert die websiteübergreifende Nutzung des Cookies. Diese Option eignet sich optimal für Anwendungen mit hohen Sicherheitsansprüchen, beispielsweise für Banken. |
| Nicht streng | Cookies mit dieser Einstellung werden nur bei Anfragen innerhalb der Website oder bei einer Navigation auf oberster Ebene mit nicht idempotenten HTTP-Anfragen wie `HTTP GET` gesendet. Daher sollte diese Option verwendet werden, wenn das Cookie von Dritten verwendet werden kann. Sie bietet einen weiteren Sicherheitsvorteil, der Benutzer vor CSRF-Angriffen schützt. |
| Keine | Cookies mit dieser Einstellung funktionieren wie die allgemein üblichen Cookies. |

Zusammengefasst werden mit Chrome 80 zwei unabhängige Einstellungen für Benutzer eingeführt: „Standard-SameSite-Cookies“ und „Cookies ohne SameSite müssen sicher sein“. Diese Einstellungen sind in Chrome 80 standardmäßig aktiviert.

![SameSite-Dialogfeld](../assets/samesite.png)

* **Standard-SameSite-Cookies**: Wenn diese Einstellung ausgewählt ist, werden alle Cookies, die das SameSite-Attribut nicht spezifizieren, automatisch gezwungen, `SameSite = Lax` zu verwenden.
* **Cookies ohne SameSite müssen sicher sein**: Wenn diese Einstellung ausgewählt ist, müssen Cookies ohne das SameSite-Attribut oder mit `SameSite = None` sicher sein. „Sicher“ bedeutet in diesem Zusammenhang, dass alle Browser-Anfragen dem HTTPS-Protokoll folgen müssen. Cookies, die diese Anforderung nicht erfüllen, werden abgelehnt. Alle Websites sollten HTTPS verwenden, um diese Anforderung zu erfüllen.

## [!DNL Target] folgt den Best Practices für die Sicherheit von Google

Bei Adobe möchten wir stets die neuesten Best Practices der Branche für Sicherheit und Datenschutz unterstützen. Deshalb freuen wir uns, Ihnen mitteilen zu können, dass [!DNL Target] die neuen von Google eingeführten Sicherheits- und Datenschutzeinstellungen unterstützt.

Für die Einstellung „Standard-SameSite-Cookies“ stellt [!DNL Target] weiterhin Personalisierungen bereit, ohne dass dies Auswirkungen auf Sie hat oder Eingriffe Ihrerseits erfordert. [!DNL Target] verwendet Erstanbieter-Cookies und funktioniert weiterhin ordnungsgemäß, da das Flag `SameSite = Lax` von Google Chrome angewendet wird.

Wenn Sie die Option „Cookies ohne SameSite müssen sicher sein“ wählen und sich nicht explizit für die Domain-übergreifende Tracking-Funktion in Target anmelden, funktionieren die Erstanbieter-Cookies in [!DNL Target] weiterhin.

Wenn Sie sich jedoch für die Verwendung des Domain-übergreifenden Trackings entscheiden, um [!DNL Target] in mehreren Domains zu nutzen, verlangt Chrome die Verwendung der Flags `SameSite = None` und „Sicher“ für Drittanbieter-Cookies. Sie müssen also sicherstellen, dass Ihre Websites das HTTPS-Protokoll verwenden. Client-seitige Bibliotheken in [!DNL Target] verwenden automatisch das HTTPS-Protokoll und hängen die Flags `SameSite = None` und „Sicher“ an Drittanbieter-Cookies in [!DNL Target] an, um sicherzustellen, dass alle Aktivitäten weiterhin ausgeführt werden.

## Was müssen Sie tun?

Um zu verstehen, was Sie tun müssen, damit [!DNL Target] weiterhin für Benutzer von Google Chrome 80 (und höher) funktioniert, sehen Sie sich die unten stehende Tabelle an, in der die folgenden Spalten angezeigt werden:

* **Target JavaScript-Bibliothek**: Wenn Sie at.js 1.*x* oder at.js 2.*x* auf Ihren Sites verwenden.
* **Standard-SameSite-Cookies = Aktiviert**: Gibt an, was passiert, wenn Ihre Besucher in Chrome „Standard-SameSite-Cookies“ aktiviert haben, welche Auswirkungen dies auf Sie hat und ob Sie etwas tun müssen, damit [!DNL Target] weiterhin funktioniert.
* **Cookies ohne SameSite müssen sicher sein = Aktiviert**: Gibt an, welche Auswirkungen es auf Sie hat, wenn Ihre Besucher „Cookies ohne SameSite müssen sicher sein“ in Chrome und höher aktiviert haben, und ob Sie etwas tun müssen, damit [!DNL Target] weiterhin funktioniert.

| Target JavaScript-Bibliothek | Standard-SameSite-Cookies = Aktiviert | Cookies ohne SameSite müssen sicher sein = Aktiviert |
| --- | --- | --- |
| at.js 1.*x* mit Erstanbieter-Cookie. | Keine Auswirkung. | Keine Auswirkung, wenn Sie kein Domain-übergreifendes Tracking verwenden. |
| at.js 1.*x* mit aktiviertem Domain-übergreifendem Tracking. | Keine Auswirkung. | Sie müssen das HTTPS-Protokoll für ihre Website aktivieren.<br />Target verwendet ein Drittanbieter-Cookie, um Benutzer zu tracken, und Google verlangt, dass Drittanbieter-Cookies die Flags &quot;`SameSite = None`&quot; und „Sicher“ verwenden. Das Flag „Sicher“ erfordert, dass Ihre Sites das HTTPS-Protokoll verwenden. |
| at.js 2.*x*  | Keine Auswirkung. | Keine Auswirkung. |

## Was muss [!DNL Target] tun?

Was mussten wir also in unserer Plattform tun, damit Sie die neuen SameSite-Cookie-Richtlinien für Google Chrome 80 und höher einhalten können?

| Target JavaScript-Bibliothek | Standard-SameSite-Cookies = Aktiviert | Cookies ohne SameSite müssen sicher sein = Aktiviert |
| --- | --- | --- |
| at.js 1.*x* mit Erstanbieter-Cookie. | Keine Auswirkung. | Keine Auswirkung, wenn Sie kein Domain-übergreifendes Tracking verwenden. |
| at.js 1.*x* mit aktiviertem Domain-übergreifendem Tracking. | Keine Auswirkung. | at.js 1.*x* mit aktiviertem Domain-übergreifendem Tracking. |
| at.js 2.*x*  | Keine Auswirkung. | Keine Auswirkung. |

## Was passiert, wenn Sie nicht zum HTTPS-Protokoll wechseln?

Das einzige Szenario, das eine Auswirkung auf Sie hat, ist, wenn Sie über at.js 1 die Domain-übergreifende Tracking-Funktion in [!DNL Target] nutzen.*x*. Wenn Sie nicht zu HTTPS wechseln, was von Google gefordert wird, werden Sie einen Anstieg der Unique Visitors in Ihren Domains feststellen, da das von uns verwendete Drittanbieter-Cookie von Google gelöscht wird. Und weil das Drittanbieter-Cookie gelöscht wird, ist [!DNL Target] nicht in der Lage, Benutzern ein konsistentes und personalisiertes Erlebnis bereitzustellen, wenn sie von einer Domain zu einer anderen navigieren. Das Drittanbieter-Cookie wird hauptsächlich zur Identifizierung eines einzelnen Benutzers verwendet, der zwischen mehreren Domains wechselt, deren Inhaber Sie sind.

## Schlussfolgerung 

Die Branche unternimmt große Anstrengungen, um das Internet für Verbraucher sicherer zu machen. Daher setzt sich Adobe mit aller Kraft dafür ein, unseren Kunden zu ermöglichen, personalisierte Erlebnisse auf eine Art und Weise bereitzustellen, durch die die Sicherheit und der Datenschutz der Endbenutzer gewährleistet ist. Sie müssen lediglich die oben genannten Best Practices befolgen und die [!DNL Target] nutzen, um die neuen SameSite-Cookie-Richtlinien von Google Chrome einzuhalten.
