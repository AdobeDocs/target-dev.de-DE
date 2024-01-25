---
keywords: Häufig gestellte Fragen zu at.js, at.js-FAQ, häufig gestellte Fragen, Flackern, Ladeprogramm, Loader, Seitenlader, domänenübergreifend, Dateigröße, x-Domäne, at.js und mbox.js, nur x, Safari, Single-Page-App, fehlende Selektoren, Selektoren, Single-Page-Anwendung, Einzelseiten-Anwendung, tt.omtrdc.net, SPA, Adobe Experience Manager, AEM, IP-Adresse, IP, httponly, HttpOnly, Secure, IP, Cookie-Domäne
description: Antworten auf häufig gestellte Fragen zu [!DNL Adobe Target] at.js-JavaScript-Bibliothek.
title: Was sind häufige Fragen und Antworten zu at.js?
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
source-git-commit: 448c43c0c10e22ad054f4ee98bfc282f8c96cdcb
workflow-type: tm+mt
source-wordcount: '2938'
ht-degree: 66%

---

# Häufig gestellte Fragen zu „at.js“

Antworten auf häufig gestellte Fragen über die [!DNL Adobe Target] zur at.js-JavaScript-Bibliothek.

## Welche Vorteile hat die Verwendung von at.js gegenüber mbox.js?

Die Bibliothek at.js ersetzt mbox.js. Die mbox.js-Bibliothek wird nicht mehr unterstützt. Für die meisten Benutzer birgt at.js jedoch Vorteile gegenüber mbox.js.

Neben anderen Vorteilen sorgt at.js für kürzere Ladezeiten von Seiten bei Webimplementierungen, bessere Sicherheit und bessere Implementierungsoptionen für Einzelseitenanwendungen.

Im folgenden Diagramm wird die Seitenladeleistung von mbox.js und at.js verglichen.

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Seitenleistungsdiagramm zum Vergleich von mbox.js mit at.js](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "Seitenleistungsdiagramm zum Vergleich von mbox.js mit at.js"){zoomable=&quot;yes&quot;}

Wie oben gezeigt, werden Seiteninhalte bei der Verwendung von mbox.js erst geladen, wenn der Aufruf von [!DNL Target] abgeschlossen wurde. Bei der Verwendung von at.js werden Seiteninhalte schon geladen, wenn der Aufruf von [!DNL Target] eingeleitet wird, nicht erst nach Abschluss des Vorgangs.

## Wie wirkt sich at.js und mbox.js auf Seitenladezeiten aus?

Viele Kunden und Berater möchten wissen, welche Auswirkungen at.js und mbox.js auf die Seitenladezeit haben, insbesondere im Zusammenhang mit neuen und wiederkehrenden Benutzern. Leider ist es schwierig, zu messen, wie sich at.js oder mbox.js auf die Seitenladezeit auswirken, und genaue Zahlen dazu anzugeben, was die Implementierung der einzelnen Kunden erfordert.

Wenn die Besucher-API jedoch auf der Seite vorhanden ist, [!DNL Target] kann besser verstehen, wie at.js und mbox.js die Seitenladezeit beeinflussen.

>[!NOTE]
>
>Die Besucher-API und at.js oder mbox.js wirken sich nur dann auf die Seitenladezeit aus, wenn Sie die globale Mbox verwenden (dies liegt an der Technik, mit der der Haupttext ausgeblendet wird). Regionale Mboxes sind von der Besucher-API-Integration nicht betroffen.

In den folgenden Abschnitten wird die Aktionssequenz für neue und zurückkehrende Besucher beschrieben:

### Neue Besucher

1. Die Besucher-API ist geladen und analysiert und wird ausgeführt.
1. at.js/mbox.js ist geladen und analysiert und wird ausgeführt.
1. Wenn die automatische Erstellung der globalen Mbox aktiviert ist, gilt für die [!DNL Target] JavaScript-Bibliothek:

   * Sie wird das Besucher-Objekt instanziieren.
   * Die [!DNL Target] -Bibliothek versucht, Experience Cloud-Besucher-ID-Daten abzurufen.
   * Weil es sich um einen neuen Besucher handelt, versendet die Besucher-API eine domänenübergreifende Anfrage an demdex.net.
   * Nach dem Abrufen der Experience Cloud-Besucher-ID-Daten wird eine Anfrage an [!DNL Target] ausgelöst wird.

### Zurückkehrende Besucher

1. Die Besucher-API ist geladen und analysiert und wird ausgeführt.
1. at.js/mbox.js ist geladen und analysiert und wird ausgeführt.
1. Wenn die automatische Erstellung der globalen Mbox aktiviert ist, gilt für die [!DNL Target] JavaScript-Bibliothek:

   * Sie wird das Besucher-Objekt instanziieren.
   * Die [!DNL Target] -Bibliothek versucht, Experience Cloud-Besucher-ID-Daten abzurufen.
   * Die Besucher-API ruft Cookie-Daten ab.
   * Nach dem Abrufen der Experience Cloud-Besucher-ID-Daten wird eine Anfrage an [!DNL Target] ausgelöst wird.

>[!NOTE]
>
>Wenn die Besucher-API vorhanden ist, [!DNL Target] muss mehrmals über die Leitung gehen, um sicherzustellen, dass [!DNL Target] -Anfragen enthalten Experience Cloud-Besucher-ID-Daten. Bei zurückkehrenden Besuchern geht [!DNL Target] nur über die Verbindung zu [!DNL Target], um den personalisierten Inhalt abzurufen.

## Warum sind die Antwortzeiten nach einem Upgrade von einer vorherigen Version von at.js auf Version 1.0.0 scheinbar langsamer?

at.js , Version 1.0.0 und neuer löst alle Anforderungen parallel aus. In den vorherigen Versionen werden die Anforderungen sequenziell ausgeführt, d. h. die Anforderungen werden in eine Warteschlange verschoben, und [!DNL Target] wartet auf den Abschluss der ersten Anforderung, bevor der Vorgang mit der nächsten Anforderung fortgesetzt wird.

Die Art und Weise, wie frühere Versionen von at.js Anforderungen ausführen, ist für das so genannte &quot;Head of Line Blocking&quot;anfällig. In at.js 1.0.0 und höher [!DNL Target] zur parallelen Anforderungsausführung gewechselt.

Wenn Sie sich beispielsweise das Wasserfallmodell der Netzwerkregisterkarte für at.js 0.9.1 ansehen, sehen Sie das nächste [!DNL Target] -Anfrage wird erst gestartet, nachdem die vorherige fertig gestellt wurde. Diese Sequenz ist bei at.js 1.0.0 und höher nicht der Fall, wo alle Anforderungen im Grunde genommen gleichzeitig beginnen.

Auf die Antwortzeit bezogen kann dies mathematisch wie folgt betrachtet werden:

<ul class="simplelist"> 
 <li> at.js 0.9.1: Reaktionszeit aller [!DNL Target] requests = Summe der Antwortzeiten von Anforderungen </li> 
 <li> at.js 1.0.0 und höher: Antwortzeit aller [!DNL Target] requests = maximum of requests response time </li> 
</ul>

Die at.js-Bibliotheksversion 1.0.0 führt die Anforderungen schneller aus. Darüber hinaus sind at.js-Anforderungen asynchron. [!DNL Target] blockiert nicht das Seiten-Rendering. Selbst wenn der Abschluss von Anforderungen mehrere Sekunden dauert, wird die gerenderte Seite angezeigt. Lediglich einige Teile der Seite bleiben leer, bis [!DNL Target] eine Antwort vom [!DNL Target]-Edge erhält.

## Kann ich die [!DNL Target]-Bibliothek asynchron laden?

In at.js 1.0.0 kann die [!DNL Target]-Bibliothek asynchron geladen werden.

So laden Sie at.js asynchron:

* Der empfohlene Ansatz erfolgt über -Tags in Adobe Experience Platform.
* Sie können at.js auch asynchron laden, indem Sie dem Skript-Tag zum Laden von at.js das asynchrone Attribut hinzufügen. Verwenden Sie etwas wie:

  ```
  <script src="<URL to at.js>" async></script>
  ```

* Sie können at.js auch mithilfe dieses Codes asynchron laden:

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

Das asynchrone Laden von at.js eignet sich hervorragend, um zu verhindern, dass das Rendern des Browsers blockiert wird. Bei dieser Technik kann es jedoch zu Flackereffekten auf der Webseite kommen.

Sie können ein Flackern vermeiden, indem Sie ein pre-hiding-Snippet verwenden, das die Seite (oder bestimmte Teile) ausblendet und diese dann nach at.js einblendet und die globale Anfrage geladen hat. Der Ausschnitt muss vor dem Laden von at.js hinzugefügt werden.

Wenn Sie at.js über eine asynchrone Implementierung bereitstellen [!UICONTROL Adobe Experience Platform] Implementieren, stellen Sie sicher, dass Sie das vorab ausgeblendete Snippet direkt auf Ihren Seiten einfügen, bevor Sie die Implementierung [!DNL Target] using [!UICONTROL Adobe Experience Platform] Einbettungscode.

Wenn Sie at.js über eine synchrone DTM-Implementierung bereitstellen, kann das vor-ausgeblendete Snippet über eine Seitenladeregel hinzugefügt werden, die oben auf der Seite ausgelöst wird.

Weitere Informationen finden Sie unter [Verwaltung von Flackern mit „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Ist at.js mit der [!DNL Adobe Experience Manager]-Integration (Experience Manager) kompatibel?

[!DNL Adobe Experience Manager] 6.2 mit FP-11577 (oder höher) unterstützt jetzt at.js-Implementierungen mit [!UICONTROL Adobe Target Cloud Service] Integration.

## Wie kann ich mit at.js ein Flackern beim Laden von Seiten verhindern ?

[!DNL Target] bietet mehrere Möglichkeiten, das Flackern beim Laden von Seiten zu verhindern. Weitere Informationen finden Sie unter [Vermeiden von Flackern mit at.js](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## Wie groß ist at.js?

Die at.js-Datei hat beim Download eine Größe von etwa 109 KB. Da die meisten Server Dateien jedoch automatisch komprimieren, um die Dateigröße zu verringern, ist at.js bei Komprimierung (mit GZIP oder einer ähnlichen Anwendung) auf dem Server etwa 34 KB groß und wird in dieser Größe auch geladen, wenn Benutzer Ihre Webseite besuchen. Die Komprimierungseinstellungen des Servers, auf dem at.js installiert ist, bestimmen die tatsächliche Größe der Datei.

## Warum ist at.js größer als mbox.js?

at.js-Implementierungen verwenden eine einzelne Bibliothek ( at.js), während mbox.js-Implementierungen tatsächlich zwei Bibliotheken verwenden ( mbox.js und target.js). Es wäre also gerechter, at.js mit mbox.js *und* `target.js` zu vergleichen. Beim Vergleich der komprimierten Größen der beiden Versionen ist ersichtlich, dass die at.js-Version 1.2 34 KB groß ist und die mbox.js-Version 63 eine Größe von 26,2 KB hat. ``

at.js ist deshalb größer, weil im Vergleich zu mbox.js deutlich mehr DOM-Parsing durchgeführt wird. Dies ist erforderlich, da at.js „Rohdaten“ in der JSON-Antwort erhält und diese zunächst verarbeiten muss. mbox.js verwendet `document.write()`, das Parsing wird vom Browser übernommen.

Trotz der größeren Datei zeigen unsere Tests, dass Seiten mit at.js schneller geladen werden als Seiten mit mbox.js. Zudem bietet at.js eine höhere Sicherheit, da keine zusätzlichen dynamischen Dateien geladen werden und `document.write` nicht benötigt wird.

## Enthält at.js jQuery? Kann ich diese Komponente von „at.js“ löschen, wenn ich jQuery bereits auf meiner Website verwende?

at.js nutzt derzeit Teile von jQuery, deshalb wird Ihnen oben in at.js der MIT-Lizenzhinweis angezeigt. jQuery wird nicht ausgelöst und die Bibliothek übt keinen Einfluss auf die bereits auf Ihrer Seite eingebettete jQuery-Bibliothek aus, bei der es sich möglicherweise um eine andere Version handelt. Der jQuery-Code in at.js lässt sich nicht löschen.

## Unterstützt „at.js“ Safari und domänenübergreifende Einstellungen, die als „nur x“ eingestellt sind?

Nein, wenn domänenübergreifend auf &quot;nur x&quot;festgelegt ist und in Safari Drittanbieter-Cookies deaktiviert sind, setzen sowohl mbox.js als auch at.js ein deaktiviertes Cookie und es werden keine Mbox-Anfragen für die Domäne dieses Kunden ausgeführt.

Um Safari-Besucher zu unterstützen, wäre eine bessere X-Domäne &quot;deaktiviert&quot;(setzt nur ein Erstanbieter-Cookie) oder &quot;aktiviert&quot;(setzt in Safari nur ein Erstanbieter-Cookie, während in anderen Browsern Erst- und Drittanbieter-Cookies gesetzt werden).

## Kann ich Target verwenden? [!UICONTROL Visual Experience Composer] (VEC) in meinen Einzelseitenanwendungen?

Ja. Sie können VEC für Ihre SPA benutzen, wenn Sie at.js 2.x verwenden. Weitere Informationen finden Sie unter [Visual Experience Composer (VEC) für Einzelseiten-Programme](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html).

## Kann ich den Adobe Experience Cloud-Debugger für at.js-Implementierungen verwenden?

Ja. Sie können außerdem mboxTrace für das Debugging oder die Entwicklerwerkzeuge Ihres Browsers verwenden und zum Isolieren von Mbox-Aufrufen nach „mbox“ filtern, um die Netzwerkanforderungen zu analysieren.

## Kann ich mit at.js Sonderzeichen in meinen Mbox-Namen verwenden ?

Ja, genau wie bei mbox.js.

## Warum werden meine Mboxes nicht auf meinen Webseiten ausgelöst?

[!DNL Target]-Kunden verwenden mitunter Cloud-basierte Instanzen mit [!DNL Target] zum Testen oder für einfache Machbarkeitsprüfungen. Diese Domänen sind neben vielen anderen Teil der [öffentlichen Suffix-Liste](https://publicsuffix.org/list/public_suffix_list.dat).

Moderne Browser speichern keine Cookies, wenn Sie diese Domänen verwenden - es sei denn, Sie passen die Einstellung `cookieDomain` mit targetGlobalSettings() an. Weitere Informationen finden Sie unter [Verwenden Cloud-basierter Instanzen mit [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md).

## Können IP-Adressen bei der Verwendung von at.js als Cookie-Domäne dienen?

Ja, wenn Sie [at.js, Version 1.2 oder neuer](/help/dev/implement/client-side/atjs/target-atjs-versions.md) verwenden. Adobe empfiehlt jedoch dringend, dass Sie mit der neuesten Version auf dem Laufenden bleiben.

>[!NOTE]
>
>Die folgenden Beispiele sind nicht notwendig, wenn Sie at.js der Version 1.2 oder neuer verwenden.

Abhängig davon, wie Sie [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) verwenden, müssen Sie möglicherweise weitere Änderungen am Code vornehmen, nachdem Sie at.js heruntergeladen haben. Benötigen Sie beispielsweise etwas voneinander abweichende Einstellungen für Ihre Implementierungen von [!DNL Target] auf verschiedenen Websites und konnten Sie diese Einstellungen nicht dynamisch mit JavaScript festlegen, nehmen Sie diese Anpassungen manuell vor, nachdem Sie die Datei heruntergeladen haben und bevor Sie sie auf der entsprechenden Website hochladen.

In den folgenden Beispielen können Sie die at.js-Funktion `targetGlobalSettings()` zum Einfügen eines Code-Ausschnitts verwenden, um IP-Adressen zu unterstützen:

Dieses Beispiel betrifft eine einzelne IP-Adresse:

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

Dieses Beispiel betrifft einen IP-Adressbereich:

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## Warum werden mir Warnhinweise wie zum Beispiel „Aktionen mit fehlenden Selektoren“ angezeigt? 

Diese Meldungen beziehen sich nicht auf die at.js-Funktionalität. Die at.js-Bibliothek versucht, alles zu melden, das nicht im DOM zu finden ist.

Nachfolgend finden Sie mögliche Grundursachen für diesen Warnhinweis:

* Die Seite wird dynamisch erstellt und at.js kann das Element nicht finden.
* Die Seite wird langsam erstellt (aufgrund eines langsamen Netzwerks) und at.js kann den Selektor im DOM nicht finden.
* Die Seitenstruktur, auf der diese Aktivität ausgeführt wird, wurde geändert. Wenn Sie die Aktivität erneut im Visual Experience Composer (VEC) öffnen, sollte Ihnen ein Warnhinweis angezeigt werden. Sie sollten die Aktivität aktualisieren, damit alle erforderlichen Elemente gefunden werden können.
* Die zugrunde liegende Seite ist Teil einer Einzelseiten-App (SPA) oder die Seite enthält Elemente, die weiter unten auf der Seite auftauchen und der at.js-&quot;Selektor-Polling-Mechanismus&quot;kann diese Elemente nicht finden. Es ist unter Umständen hilfreich, den `selectorsPollingTimeout` zu erhöhen. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Eine beliebige Klick-Tracking-Metrik versucht, sich zu jeder Seite hinzuzufügen, unabhängig von der URL, in der die Metrik eingerichtet wurde. Diese Situation ist zwar harmlos, hat aber viele dieser Warnhinweise zur Folge.

  Die besten Ergebnisse erzielen Sie, wenn Sie die [aktuelle Version von at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md). Weitere Informationen zum Herunterladen von &quot;at.js&quot;finden Sie unter [Herunterladen von at.js mithilfe der [!DNL Target] Benutzeroberfläche](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) im Abschnitt [*Implementieren von &quot;at.js&quot;* > *Implementierung [!DNL Target] ohne Tag-Manager*](how-to-deployatjs/implement-target-without-a-tag-manager.md) Artikel.

## Was ist die Domain tt.omtrdc.net, zu der die Aufrufe des [!DNL Target]-Servers gehen?

tt.omtrdc.net ist der Domänenname für das Adobe EDGE-Netzwerk, mit dem alle Server-Aufrufe für [!DNL Target].

## Warum verwendet at.js nicht immer die Cookie-Flags „HttpOnly“und „Secure“?

„HttpOnly“ kann nur über Server-seitigen Code festgelegt werden. [!DNL Target]-Cookies, wie z. B. Mbox, werden über JavaScript-Code erstellt und gespeichert, also kann [!DNL Target] Cookieflag „HttpOnly“ nicht verwenden. [!DNL Target] verwendet set HttpOnly für Drittanbieter-Cookies, die Server-seitig gesetzt werden, wenn domänenübergreifend aktiviert.

„Secure“ kann nur über JavaScript festgelegt werden, wenn die Seite mit HTTPS geladen wurde. Wenn die Seite nur mit HTTP geladen wird, kann JavaScript dieses Flag nicht festlegen. Darüber hinaus ist das Cookie bei der Verwendung des Flags „Secure“ nur auf HTTPS-Seiten verfügbar. Für Seiten, die über HTTPS geladen werden, legt [!DNL Target] die Attribute Secure und SameSite=None fest.

Um sicherzustellen, dass [!DNL Target] Benutzer ordnungsgemäß verfolgen kann und die Cookies Client-seitig generiert werden, verwendet [!DNL Target] keine dieser Flags außer in den oben genannten Situationen.

## Wie behandelt at.js Sicherheitsprobleme wie XSS- und MITM-Angriffe?

Die Kommunikation mit dem Adobe Edge-Netzwerk, das von at.js aktiviert wird, erfolgt nur über HTTPS, solange die Variable `secureOnly` ist in der Funktion targetGlobalSettings() auf true gesetzt ([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)), andernfalls darf at.js basierend auf dem Seitenprotokoll zwischen HTTP und HTTPS wechseln.

Die folgenden Header werden standardmäßig erzwungen:
* HTTP Strict Transport Security (HSTS)
* X-XSS-Schutz
* X Content-Typ-Optionen
* Referrer-Richtlinie

Alle Header, die bereits in Client-Seiten verwendet werden, können erzwungen werden. Eine gängige Methode hierfür ist die &quot;HTTP Request Header Authorization&quot;. Die Adobe-Kundenunterstützung kann weitere Informationen zu Best Practices erhalten.

Darüber hinaus sind Anfragen an das Adobe Edge-Netzwerk öffentlich (da sie für Besucherbrowser konzipiert sind) und enthalten keine sichtbaren Besucherdetails (sie enthalten nur eine Besucher-ID). Diese Anforderungen stellen Besuchern Erlebnisse bereit und enthalten Details dazu, was ein Besucher auf der Seite sehen sollte.

Beachten Sie, dass für Antwort-Token und Sitzungs-IDs, die in diesen Anfragen übertragen werden, Folgendes gilt:

* Sie verfolgen Kommunikationssitzungen
* Sie bestehen aus zufälligen Zeichen
* Sitzungs-IDs sind 30 Minuten lang gültig.
* Antwort-Token können deaktiviert werden ([Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html))
* Sie sind nur in der Umgebung von Adobe-Lösungen nützlich.

Es wird erwartet, dass die `Access-Control-Allow-Origin` -Kopfzeile mit dem Wert &quot;*&quot;in at.js-Anforderungen verwenden, da sie öffentlich sind, ist keine Authentifizierung erforderlich und der Zugriff auf das Adobe Edge-Netzwerk muss über JavaScript-Aufrufe von jeder Domäne aus erfolgen.

Content Security Policy (CSP) muss jedoch auf der Seite erzwungen werden. Weitere Informationen zu CSP-Anforderungen für at.js finden Sie unter [Inhaltssicherheitsrichtlinie](/help/dev/before-implement/privacy/content-security-policy.md) und [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Wie oft sendet at.js Netzwerkanfragen? 

Die [!DNL Target] gesamte Entscheidungsfindung von findet Server-seitig statt. Das bedeutet, dass at.js jedes Mal, wenn die Seite neu geladen oder eine öffentliche at.js-API aufgerufen wird, eine Netzwerkanfrage gesendet wird.

## Können wir im besten Fall davon ausgehen, dass Benutzer durch das Ausblenden, Ersetzen und Wiedereinblenden von Inhalten keine Beeinträchtigung der Seitenladezeit bemerken werden?

at.js vermeidet das Vorab-Ausblenden des HTML-Bodys oder anderer DOM-Elemente über einen längeren Zeitraum, dies ist jedoch von den Netzwerkbedingungen und der Aktivitätseinrichtung abhängig. at.js bietet [Einstellungen](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md), mit denen Sie den CSS-Style zum Ausblenden des Bodys anpassen können, um nicht den gesamten HTML-Body, sondern nur bestimmte Teile der Seite auszublenden. Hierbei wird erwartet, dass diese Teile DOM-Elemente enthalten, die „personalisiert“ werden müssen.

## Wie lautet die Reihenfolge der Ereignisse in einem durchschnittlichen Szenario, in dem sich ein Benutzer für eine Aktivität qualifiziert? 

Bei der at.js-Anfrage handelt es sich um eine asynchrone `XMLHttpRequest`, weshalb wir folgende Schritte ausführen:

1. Die Seite wird geladen.
1. at.js blendet den HTML-Body vorab aus. Es gibt eine Einstellung, mit der sich anstelle des gesamten HTML-Bodys nur ein bestimmter Container ausblenden lässt.
1. Die at.js-Anfrage wird gesendet.
1. Nachdem die [!DNL Target]-Antwort eingegangen ist, extrahiert [!DNL Target] die CSS-Selektoren.
1. Mit den CSS-Selektoren erstellt [!DNL Target] STYLE-Tags, um die anzupassenden DOM-Elemente vorab auszublenden.
1. Der STYLE zum Vorab-Ausblenden des HTML-Bodys wird entfernt.
1. [!DNL Target] beginnt mit dem Abrufen der DOM-Elemente.
1. Wenn ein DOM-Element gefunden wird, wendet [!DNL Target] DOM-Änderungen an und der STYLE zum Vorab-Ausblenden des Elements wird entfernt.
1. Wenn keine DOM-Elemente gefunden werden, werden durch ein globales Timeout alle Elemente eingeblendet, um Seitenfehler zu verhindern.

## Wie oft war der Seiteninhalt vollständig geladen und sichtbar, wenn at.js das Element, das durch die Aktivität geändert wird, zum letzten Mal einblendet?

Wie oft war der Seiteninhalt im oben aufgeführten Szenario vollständig geladen und sichtbar, wenn at.js das Element, das durch die Aktivität geändert wird, zum letzten Mal einblendet? Anders ausgedrückt: Die Seite ist vollständig sichtbar, ausgenommen der Aktivitätsinhalt, der kurz nach dem anderen Inhalt eingeblendet wird.

at.js blockiert nicht das Seiten-Rendering. Benutzer bemerken möglicherweise leere Bereiche auf der Seite, in denen sich die von [!DNL Target] angepassten Elemente befinden. Wenn der anzuwendende Inhalt nicht viele Remote-Assets, wie z. B. Skripte oder Bilder, enthält, wird alles schnell dargestellt.

## Wie wirkt sich eine vollständig zwischengespeicherte Seite auf das oben aufgeführte Szenario aus? Ist es in diesem Fall wahrscheinlicher, dass der Aktivitätsinhalt merklich nach dem Rest des Seiteninhalts geladen wird? 

Wenn eine Seite in einem CDN gespeichert ist, das sich nahe am Standort des Benutzers, aber nicht in der Nähe des [!DNL Target]-Edge befindet, erlebt dieser Benutzer möglicherweise Verzögerungen. [!DNL Target]-Edges sind jedoch über die ganze Welt verteilt, sodass dies in der Regel kein Problem darstellt.

## Ist es möglich, ein Hero-Bild anzuzeigen, das nach kurzer Verzögerung ersetzt wird? 

Stellen Sie sich folgendes Szenario vor:

Das [!DNL Target]-Timeout beträgt fünf Sekunden. Ein Benutzer lädt eine Seite, die eine Aktivität zum Anpassen des Hero-Bilds aufweist. at.js sendet die Anfrage, um zu bestimmen, ob eine Aktivität angewendet werden muss, die erste Antwort bleibt jedoch aus. Wir können also davon ausgehen, dass der Benutzer den regulären Inhalt des Hero-Bilds sieht, da keine Antwort von [!DNL Target] zu etwaigen anzuwendenden Aktivitäten eingegangen ist. Nach vier Sekunden gibt [!DNL Target] eine Antwort mit den Aktivitätsinhalten zurück.

Ist es zu diesem Zeitpunkt möglich, dass die alternative Version angezeigt wird? Nach vier Sekunden könnte das Hero-Bild also ausgetauscht werden. Würde der Benutzer diesen Austausch bemerken?

Das Hero-DOM-Element ist zu Beginn ausgeblendet. Nachdem eine Antwort von [!DNL Target] eingeht, wendet at.js die DOM-Änderungen an, wie z. B. die IMG-Änderung und die Anzeige des angepassten Hero-Bilds.

## Welcher HTML-Doctype ist für at.js erforderlich?

at.js erfordert den Doctype HTML 5.

Diese Syntax lautet:

`<!DOCTYPE html>`

Der Doctype HTML 5 stellt sicher, dass die Seite im Standardmodus geladen wird. Beim Laden im Quirks-Modus sind einige JS-APIs, von denen at.js abhängig ist, deaktiviert. [!DNL Target] deaktiviert at.js im Quirks-Modus.

## Funktioniert at.js in einer Ionic-App-Umgebung.

Diese Implementierung wurde nie getestet, da at.js nicht für die Verwendung in einer Nicht-Web-Umgebung vorgesehen war. [!DNL Adobe] empfiehlt [SDKs für mobile Implementierungen](/help/dev/implement/mobile/overview.md).
