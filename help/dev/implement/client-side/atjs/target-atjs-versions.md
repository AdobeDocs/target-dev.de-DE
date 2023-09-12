---
keywords: at.js-Versionen, at.js-Versionen, Versionshinweise
description: Details zu Änderungen in den einzelnen Versionen der [!DNL Adobe Target] at.js-JavaScript-Bibliothek.
title: Was ist in den einzelnen Versionen von at.js enthalten?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: 0bdbeebc07bc4e1dd0dc34171fbf2476db5c256f
workflow-type: tm+mt
source-wordcount: '4635'
ht-degree: 73%

---

# „at.js“-Versionsdetails

Details zu den Änderungen in den einzelnen Versionen der at.js-JavaScript-Bibliothek von [!DNL Adobe Target]

>[!IMPORTANT]
>
>[!DNL Adobe Target] unterstützt beide at.js 1.*x* und at.js 2.*x*.
>
>at.js 1.*x*   in den Wartungsmodus versetzt wurde. Die [!DNL Target] Team veröffentlicht bei Bedarf Fehlerbehebungen und Sicherheits-Patches.
>
>Die [!DNL Target] -Team bietet vollständige Unterstützung für at.js 2.*x* und veröffentlicht fortlaufend Fehlerbehebungen, Sicherheits-Patches, Funktionen und Leistungsoptimierung.
>
>Sie sollten auf die neuesten Versionen von einem der beiden 1 aktualisieren.*x* las 2.*x* um Fehlerbehebungen und Sicherheits-Patches für Probleme zu erhalten, die in einer früheren Nebenversion der entsprechenden Hauptversion entdeckt wurden.

Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sind die bevorzugte Methode zum Aktualisieren von at.js. Erweiterungsentwickler fügen ihren Erweiterungen kontinuierlich neue Funktionen hinzu und beheben häufig Fehler. Diese Aktualisierungen werden in neuen Versionen einer Erweiterung zusammengefasst und im Adobe Experience Platform-Katalog als Aktualisierungen bereitgestellt. Weitere Informationen finden Sie unter [Erweiterungs-Upgrades](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html) im *Übersicht über Tags* guide.6+

## at.js-Version 2.10.3 (12. September 2023)

* Fehlerkorrektur - Die `at-content-rendering-succeeded` benutzerspezifisches Ereignis, wenn keine Angebote gerendert werden. das richtige Ereignis, `at-content-rendering-no-offers`, wird jetzt ausgelöst.
* hinzugefügt `eventToken` und `responseTokens` zum Fehlerobjekt für die `at-content-rendering-failed` benutzerspezifisches Ereignis.

## at.js-Version 2.10.2 (7. März 2023)

* Es wurde ein Fehler behoben, der dazu geführt hatte, dass die Funktion `trackEvent` immer einen Fehler zurückgab.

## at.js-Version 2.10.1 (2. Februar 2023)

* Es wurde ein Fehler behoben, durch den Aktivitäten in Verbindung mit Zielgruppenregeln, die Parameter mit Punkten in ihren Namen enthielten, beim On-Device Decisioning nicht das erwartete Erlebnis zurückgaben.
* Es wurde ein Fehler behoben, der in at.js 2.6.0 eingeführt wurde und in dem at.js einen Bereitstellungsaufruf auslöste, selbst wenn mboxDisable aktiviert war.

## at.js-Version 2.10.0 (19. September 2022)

* Unterstützung von Drittanbieter-Cookies hinzugefügt.

## at.js-Version 2.9.0 (27. Mai 2022)

* Unterstützung für [User Agent Client Hints](user-agent-and-client-hints.md) wurde hinzugefügt.
* Es wurde ein Fehler behoben, durch den mehrere Mbox-Anfragen auf derselben Seite unterschiedliche Impressions-IDs erhielten.

## at.js-Version 2.8.1 (28. Januar 2022)

* Es wurde ein Problem behoben, wo `pageLoad` im hybriden Ausführungsmodus On Device Decisioning (ODD) nicht auf target-global-mbox abgebildet wurde.
* Es wurde ein Problem mit Analysedetails für mbox-Anfragen behoben.
* Dev-Abhängigkeiten wurden aktualisiert, um Sicherheitslücken zu beheben.

## at.js-Version 2.8.0 (7. Januar 2022)

Die at.js-JavaScript-Bibliothek von [!DNL Target] erfasst jetzt Daten zur Nutzung von Funktionen und Daten der Leistungsmessung. Personenbezogene Daten werden nicht erfasst. Eine Abwahl dieser Funktion ist verfügbar, indem `telemetryEnabled` in `targetGlobalSettings` auf „false“ gesetzt wird. Weitere Informationen finden Sie unter [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).

## at.js-Version 2.7.0 (28. Oktober 2021)

Diese Version enthält die folgende Verbesserung:

* Hinzugefügte Unterstützung für [Web-Komponenten](https://developer.mozilla.org/de/docs/Web/Web_Components). Diese Version von at.js ist erforderlich, um personalisierte Erlebnisse und Angebote für benutzerdefinierte Elemente und Elemente innerhalb von benutzerdefinierten Elementen zu erstellen und zu testen. Diese Funktion ist in der Version 21.10.5 von [!DNL Target Standard/Premium] enthalten.

## at.js 1.8.3 (21. September 2021)

Diese Version enthält die folgenden Änderungen:

* Entfernt die `reactor-window` und `reactor-document` Adobe Experience Platform Launch-Module, um sicherzustellen, dass die Platform launch-Erstellung für Kunden mit `window.default` oder `document-default` festgelegt ist.
* at.js 1.8.3 setzt jetzt explizit `Samesite=None` und `Secure` , um sicherzustellen, dass Drittanbieter-Domain-Cookies ordnungsgemäß gesetzt werden.

## at.js 2.6.1 (16. August 2021)

* Fehlerbehebung für „Für den Hybrid-Modus ist kein zwischengespeichertes Artefakt verfügbar“ bei Verwendung der geräteinternen Entscheidungsfindung.

## at.js 2.6.0 (16. Juli 2021)

* Das Attribut „secure“ wurde zu Cookies hinzugefügt für alle Fälle, in denen die at.js-Einstellungen `secureOnly` auf `true` gesetzt sind.
* Bei Verwendung von `triggerView()` sind jetzt Antwort-Token verfügbar.
* Es wurde ein Problem im Zusammenhang mit dem Ereignis `CONTENT_RENDERING_NO_OFFERS` behoben. Jetzt wird dieses Ereignis korrekt ausgelöst, wenn kein Inhalt von [!DNL Target] zurückgegeben wird.
* [!UICONTROL Analytics for Target] (A4T) Klickmetrikdetails werden bei Verwendung von `prefetch` -Anfragen.
* Die UUID-Generierung verwendet nicht mehr `Math.random()`, sondern beruht auf `window.crypto`.
* Der Ablauf des `sessionId`-Cookies wird bei jedem Netzwerkaufruf korrekt verlängert.
* Die Ansichts-Cache-Initialisierung für die Einzelseiten-Anwendung (SPA, Single Page Application) wird jetzt korrekt verarbeitet und berücksichtigt die Einstellungen `viewsEnabled`. Einstellung `viewsEnabled` der `false` Wert deaktiviert jetzt die `triggerView()` -Funktion. Siehe [Reihenfolge der Vorgänge beim ersten Laden der Seite](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order).

## at.js 2.5.0 (13. Mai 2021)

Diese Version von at.js umfasst die folgenden Verbesserungen und Änderungen:

* Unterstützung der [geräteinternen Entscheidungsfindung](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) für at.js.
* Unterstützung für [Vorschau-Links](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) für Automated Personalization-Aktivitäten

Mit dieser Version endet auch die Unterstützung für Microsoft Internet Explorer 10 und höher.

## at.js 2.4.1 (23. März 2021)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Es wurde ein Problem behoben, bei dem `targetPageParams` in Mbox-Anfragen enthalten waren. `targetPageParams` sollten nur in `pageLoad`-Anfragen enthalten sein. (TNT-40247)
* Optimierte Fenster- und Dokumentglobal-Verweise in der Adobe Experience Platform-Erweiterung. (TNT-37124)

## at.js 2.4.0 (14. Januar 2021)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Fehlerbehebungen enthält:

* Fügt Unterstützung für die einheitliche Profil-/Plattform-ID zu den Bereitstellungs-API-Kunden-IDs hinzu.
* Die fehlerhafte Style-Tag-Injektion wurde behoben.

## at.js 2.3.3 (13. November 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgende Fehlerbehebung enthält:

* Es wurde ein Problem im Zusammenhang mit mbox click tracking und A4T behoben. Mit 0n-Klick [!DNL Target] Es wurde ein API-Aufruf zum Versand mit den richtigen Mbox- und Mbox-Parametern ausgelöst. Die SDID stimmte jedoch nicht mit der im [!DNL Analytics] -Aufruf, sodass keine Trefferzuordnung und -konvertierung erfolgte. (TNT-38372)

## at.js 2.3.2 (24. Juli 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgende Fehlerbehebung enthält:

* Ein Fehler wurde behoben, der auftrat, wenn dem Fenster oder Dokument durch ein Skript oder Code eine Standardeigenschaft hinzugefügt wurde.

## at.js 1.8.2 (15. Juni 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgende Fehlerbehebung enthält:

* Ein Problem wurde behoben, dass dazu führte, dass at.js 1.*x* bei Verwendung von CNAME und eines Edge-Override die Serverdomäne nicht korrekt erstellte, wodurch die [!DNL Target]-Anforderung fehl schlug. (TNT-35064)

## at.js 2.3.1-Versionen (15. Juni 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Die Einstellung `deviceIdLifetime` kann nun mit [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) überschrieben werden. (TNT-36349)
* Ein Problem wurde behoben, dass dazu führte, dass at.js 2.*x* bei Verwendung von CNAME und eines Edge-Override die Serverdomäne nicht korrekt erstellte, wodurch die [!DNL Target]-Anforderung fehl schlug. (TNT-35065)
* Es wurde ein Problem bei der Verwendung der Variablen [!DNL Target] Erweiterung v2 und [!UICONTROL Adobe Analytics Launch] Erweiterung, [!DNL Target] verzögert die [!DNL Analytics] `sendBeacon` aufrufen. (TNT-36407, TNT-35990, TNT-36000)

## at.js-Version 2.3.0 (25. März 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Unterstützung für das Festlegen von Content Security Policy-Nonces für SCRIPT- und STYLE-Tags, die beim Anwenden der bereitgestellten Inhalte an das Seiten-DOM angehängt werden [!DNL Target] Angebote. Kunden können `targetGlobalSettings.cspScriptNonce` und `targetGlobalSettings.cspStyleNonce` damit at.js die entsprechenden Skript- und Stil-Tag-Nonces für angewendete Angebote festlegen kann. Siehe  [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) für weitere Details.
* Es wurde ein Problem beim Kompilieren von at.js mit dem Google Closure-Compiler für die Implementierung von Google Tag Manager behoben.
* &quot;at.js&quot;-Cookie für die Prüfung von `check` nach `at_check` um Kollisionen mit den Implementierungen der Kunden zu vermeiden.

## at.js-Version 1.8.1 (25. März 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* &quot;at.js&quot;-Cookie für die Prüfung von `check` nach `at_check` um Kollisionen mit den Implementierungen der Kunden zu vermeiden.

## at.js-Version 2.2.0 (10. Oktober 2019)

Diese Version von at.js umfasst die folgenden Erweiterungen und Fehlerbehebungen:

* Es wurde ein Problem behoben, bei dem bei Klick-Tracking keine Konversionen in [!DNL Analytics for Target] (A4T) wann [!DNL Adobe Analytics] -Code war in Seitenelementen nicht vorhanden.
* Die Leistung bei der Verwendung von Experience Cloud ID Service (ECID) v4.4 und at.js 2.2 auf Ihren Webseiten wurde verbessert.
* Bislang führte ECID zwei Sperraufrufe durch, bevor at.js Erlebnisse abrufen konnte. Dies wurde auf einen Aufruf reduziert, wodurch die Leistung deutlich verbessert wurde.
* Fehlerkorrektur - Die Verarbeitung vorab abgerufener Ansichten funktioniert jetzt ordnungsgemäß, wenn Ereignis-Token aus Standardangeboten nicht in gesendeten Benachrichtigungen enthalten sind.

>[!NOTE]
>
>Aktualisieren Sie Ihre ECID-Erweiterung auf Version 4.4, um diese Leistungsverbesserung nutzen zu können.

* at.js , Version 2.2 bietet außerdem eine neue Einstellung mit dem Namen `serverState`. Diese Einstellung kann verwendet werden, um die Seitenleistung zu optimieren, wenn eine hybride Integration von [!DNL Target] implementiert wurde. Hybride Integration bedeutet, dass Sie sowohl at.js v2.2+ auf Client-Seite als auch die Bereitstellungs-API oder eine [!DNL Target] SDK auf Server-Seite, um Erlebnisse bereitzustellen. `serverState` ermöglicht at.js v2.2+, Erlebnisse direkt aus Inhalten anzuwenden, die auf Serverseite abgerufen und als Teil der bereitzustellenden Seite an den Client zurückgegeben wurden. Weitere Informationen finden Sie unter „serverState“ in [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate).

## at.js-Version 1.8.0 (10. Oktober 2019)

Diese Version von at.js umfasst die folgenden Erweiterungen und Fehlerbehebungen:

* Die Leistung bei der Verwendung von Experience Cloud ID Service (ECID) v4.4 und at.js 1.8 auf Ihren Webseiten wurde verbessert.
* Bislang führte ECID zwei Sperraufrufe durch, bevor at.js Erlebnisse abrufen konnte. Dies wurde auf einen Aufruf reduziert, wodurch die Leistung deutlich verbessert wurde.

>[!NOTE]
>
>Aktualisieren Sie Ihre ECID-Erweiterung auf Version 4.4, um diese Leistungsverbesserung nutzen zu können.

## at.js Version 2.1.1 (24. Juli 2019)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

(Die Problemnummern in Klammern dienen internen Adobe-Benutzern.)

* Es wurde ein Problem behoben, durch das mehrere Beacons ausgelöst wurden, wenn die Klick-Tracking-Metrik auf der Seite „Ziele und Einstellungen“ im Visual Experience Composer (VEC) verwendet wurde. (TNT-32812)
* Es wurde ein Problem behoben, durch das `triggerView()` Angebote nicht öfter als einmal gerendert hat. (TNT-32780)
* Es wurde ein Problem mit `triggerView()` behoben, sodass Anfragen jetzt Experience Cloud ID (ECID)-Informationen enthalten. (TNT-32776)
* Es wurde ein Problem behoben, durch das die `triggerView()`-Benachrichtigung auch dann nicht ausgelöst wurde, wenn keine gespeicherten Ansichten vorhanden waren. (TNT-32614)
* Es wurde ein Fehler behoben, der aufgrund der Verwendung von decodeURIcomponent auftrat, wenn die URL einen falsch formatierten Abfragezeichenparameter enthielt. (TNT-32710)
* Das Beacon-Flag ist nun im Kontext von Versandanfragen, die über die `Navigator.sendBeacon()`-API gesendet werden, auf „true“ gesetzt. (TNT-32683)
* Es wurde ein Problem behoben, durch das Recommendations-Angebote für manche Kunden nicht auf Websites angezeigt wurden. Kunden konnten den Angebotsinhalt im Bereitstellungs-API-Aufruf sehen, das Angebot wurde jedoch nicht auf der Website angewendet. (TNT-32680)
* Es wurde ein Problem behoben, durch das Klick-Tracking erlebnisübergreifend nicht wie erwartet funktionierte. (TNT-32644)
* Es wurde ein Problem behoben, durch das at.js die zweite Metrik nicht mehr anwenden konnte, wenn die Darstellung der ersten Metrik fehlgeschlagen war. (TNT-32628)
* Es wurde ein Problem beim Weiterleiten der `mbox3rdPartyId` mit der Funktion `targetPageParams` behoben, was dazu geführt hatte, dass die Payload der Anfrage weder in den Abfrageparametern noch in der Payload der Anfrage vorhanden war. (TNT-32613)
* Es wurde ein Problem behoben, durch das die Antworten auf Anzeige- und Klick-Benachrichtigungen in Chromium-basierten Browsern blockiert wurden (einschließlich Google Chrome). (TNT-32290)

## at.js-Version 2.1.0 (3. Juni 2019)

Dieses Release umfasst die folgenden Funktionen und Erweiterungen:

* **Die Opt-In-Unterstützung von Adobe**: Die Opt-In-Unterstützung bietet die Möglichkeit, Adobe-Lösungsintegrationen mit Genehmigungsverwaltungsplattformen zu vereinfachen. Weitere Informationen zu Adobe Opt-In finden Sie unter [Privatsphäre und Datenschutz-Grundverordnung (DSGVO)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

* **Kompatibel mit dem Branchenstandard CSP**: at.js verwendet nicht mehr eval(), um JavaScript auszuführen.

* **Clientseitige Analyseprotokollierung**: Ermöglicht Kunden die vollständige Kontrolle darüber, wie sie Analysedaten an senden möchten. [!DNL Adobe Analytics], ob Client- oder Server-seitig.

  Weitere Informationen finden Sie unter [Client-seitig [!DNL Analytics] Protokollierung](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side).

* **Benachrichtigungen senden**: Erlauben Entwicklern, Benachrichtigungen zu senden, wenn ein Erlebnis durch ihren Code statt über `applyOffer()` oder `applyOffers()` gerendert wird.

  Weitere Informationen finden Sie unter [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md).

* **at.js-Größe um ~ 24 % verringert**: Die Größe von at.js wurde um ~ 24 % verringert. Die kleinere Dateigröße verbessert die Seitenladeleistung und verringert die Ladedauer von at.js auf der Seite.

## at.js-Version 2.0.1 (19. März 2019)

Dies ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

(Die Problemnummern in Klammern dienen internen Adobe-Benutzern.)

* Es wurde eine Race-Bedingung im DOM-Polling-Code behoben, durch die JavaScript-Ausnahmen für bestimmte Kunden verursacht wurden. (TNT-31869)
* Benachrichtigungen, die angezeigt wurden, wurden von Click-Tracking-Ereignishandlern entkoppelt. Zunächst [!DNL Target] keine Benachrichtigungen gesendet, wenn Click-Event-Handler, die zu einer gerenderten Ansicht gehören, nicht angehängt werden konnten. [!DNL Target] sendet jetzt eine Ansichtsbenachrichtigung, auch wenn Klickelemente nicht gefunden werden. (TNT-31969)
* Es wurde ein Fehler behoben, der dazu führte, dass das Ereignisumleitungsflag „request-succeeded“ immer auf „true“ gesetzt wurde. (TNT-31907)
* Es wurde ein Problem behoben, durch das die VEC-Neuanordnungs-Aktion als Erfolg protokolliert wurde, selbst wenn Elemente fehlen. (TNT-31924)
* Es wurde ein Problem behoben, durch das Benachrichtigungen für bestimmte Kunden das Eigenschafts-Token für die Unternehmensberechtigungen nicht enthalten. (TNT-31999)

## at.js-Version 1.7.1 (19. März 2019)

Diese Version ist eine Wartungsversion und beinhaltet die folgenden Fehlerbehebungen:

(Die Problemnummern in Klammern dienen internen Adobe-Benutzern.)

* Es wurde eine Race-Bedingung im DOM-Polling-Code behoben, durch die JavaScript-Ausnahmen für bestimmte Kunden verursacht wurden. (TNT-31869)

## „at.js“-Version 2.0.0

at.js 2.x bietet umfassende Funktionen mit denen Ihr Unternehmen mithilfe von Client-seitigen Technologien der neuesten Generation Personalisierungen ausführen kann. Diese neue Version konzentriert sich auf die Aktualisierung von at.js, um harmonische Interaktionen mit Einzelseitenanwendungen (SPAs) zu ermöglichen.

Hier einige Vorteile der Verwendung von at.js 2.x, die in früheren Versionen nicht verfügbar sind:

* Die Möglichkeit, alle Angebote beim Laden der Seite zwischenzuspeichern, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren.
* Drastische Verbesserung der Erlebnisse Ihrer Endbenutzer auf Ihrer Site, da Angebote sofort über den Cache angezeigt werden, ohne dass die herkömmlichen Server-Aufrufe verzögert werden.
* Einfache einzeilige Code- und Einmalentwickler-Einrichtung, um Ihren Marketingmitarbeitern die Erstellung und Ausführung von A/B- und Experience-Aktivitäten (XT) über Visual Experience Composer (VEC) auf Einzelseitenanwendungen zu ermöglichen.

at.js 2.x enthält die folgenden neuen Funktionen:

* getOffers()
* applyOffers()
* triggerView()

Die folgenden Funktionen sind mit der Einführung von at.js 2.x veraltet:

* mboxCreate()
* mboxDefine
* registerExtension()

Weitere Informationen finden Sie unter [Aktualisieren von at.js 1.x auf at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) und [at.js-Funktionen](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>Wenn Sie Adobe Opt-in-Unterstützung für die [Die Datenschutz-Grundverordnung](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (DSGVO) müssen Sie derzeit at.js 1.7.0 oder at.js 2.1.0 oder höher verwenden.

## „at.js“-Version 1.7.0

at.js 1.7.0 bietet Adobe Opt-in-Unterstützung. Adobe Opt-In bietet die Möglichkeit, Adobe-Lösungsintegrationen mit Genehmigungsverwaltungsplattformen zu vereinfachen.

Weitere Informationen zu Adobe Opt-in finden Sie unter [Privatsphäre und Datenschutz-Grundverordnung (DSGVO)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

Diese Version behebt auch ein Problem, bei dem [!DNL Target] kann Umleitungs-URL-Parameter mit Parametern überschreiben, die aus der Umleitungs-URL stammen.

>[!NOTE]
>
>Wenn Sie Adobe Opt-in-Unterstützung für die DSGVO benötigen, müssen Sie derzeit at.js 1.7.0 oder at.js 2.1.0 oder höher verwenden.

## „at.js“-Version 1.6.4

at.js 1.6.4 ist eine Wartungsversion, die folgendes Problem behebt:

* Es wurde eine Race-Bedingung in Microsoft Internet Explorer 11 behoben, die dazu führte, dass doppelte Angebote angewendet wurden.

## „at.js“-Version 1.6.3

at.js, Version 1.6.3, enthält die folgenden Fehlerbehebungen und Verbesserungen:

* Selektoren sind jetzt CSS-escaped, wenn sie IDs oder CSS-Klassen enthalten, die mit einer Ziffer, zwei Bindestrichen oder einem Bindestrich, gefolgt von einer Ziffer (z. B. #-123), beginnen. (TNT-31061)
* Es wurde ein Problem behoben, das mit at.js 1.6.2 eingeführt wurde: Angebote von Visual Experience Composer (VEC) aus verschiedenen Aktivitäten, die für denselben CSS-Selektor gelten, berücksichtigten nicht die Aktivitätenpriorität. (TNT-31052)
* Es wurde ein Problem behoben, bei dem Zeitüberschreitungen für Zusagen in Umgebungen auftraten, in denen Zusagen nativ nicht unterstützt werden. (TNT-30974)
* Probleme werden jetzt korrekt erfasst und über das Ereignis „Inhaltswiedergabe fehlgeschlagen“ gemeldet. Zuvor wurde unter Umständen gemeldet, dass JavaScript erfolgreich ausgeführt wurde, selbst wenn dies nicht der Fall war. (TNT-30599)

## „at.js“-Version 1.6.2

Dies ist eine Wartungsversion, die folgendes Problem behebt:

* Es wurde ein Problem behoben, das auf einigen Kundensites auftrat und bei dem eine „asynchrone“ Endlosschleife auftrat.

>[!WARNING]
>
>Darüber hinaus enthält at.js, Version 1.6.2, auch alle Verbesserungen und Fehlerbehebungen der Versionen 1.6.1 und 1.6.0. Diese Versionen stehen nicht mehr zum Download zur Verfügung. Wenn Sie noch Version 1.6.1 oder 1.6.0 verwenden, empfehlen wir ein Upgrade auf Version 1.6.2

Im Folgenden finden Sie einige Verbesserungen und Fehlerbehebungen in „at.js“-Version 1.6.1:

* Es wurde ein Problem in Version 1.6.0 behoben, bei dem Recommendations-Erlebnisse in Microsoft Internet Explorer 11 dupliziert wurden. (TNT-30593)
* „at.js“ stellt jetzt sicher, dass die Edge Logikprüfungen hinsichtlich der Verfügbarkeit eines Edge-Cluster-Cookies überschreiben kann, um unterschiedliche Edge-Nummern zu verhindern, wenn Benutzer während einer Sitzung zwischen Edges wechseln. (TNT-30563)
* Es wurde ein Problem behoben, bei dem „at.js“ keine nachfolgenden Aktionen durchführte, wenn der HTML-Inhalt ungültigen JS-Code enthielt. „at.js“ protokolliert jetzt jeden Fehler und rendert die verbleibenden Aktionen ohne Probleme. (TNT-30546)
* Es wurden Änderungen vorgenommen, damit eine Ausnahme auftritt, wenn eine Umleitungsseite sich erneut für eine Umleitungsaktivität qualifiziert. (TNT-30532)
* Es wurde ein Problem behoben, bei dem über die API-Anfrage „getOffer()“ nicht das richtige Anfrage-Timeout abgerufen wurde. (TNT-30498)
* Es wurde ein Problem in „at.js“-Version 1.6.0 behoben, bei dem das Speichern von Cookies bei der Verwendung des Dateiprotokolls nicht möglich war. (TNT-30454)
* Es wurde ein Problem behoben, bei dem angezeigt wurde, dass bei Verwendung von [!DNL Analytics for Target] (A4T). (TNT-30444)
* Es wurde ein Fehler behoben, der dazu führte, dass die Seite nach dem [!DNL Target] -Aufruf ist erfolgreich. (TNT-30358)

Im Folgenden finden Sie einige Verbesserungen und Fehlerbehebungen in „at.js“-Version 1.6.0:

* Umleitungsangebote werden jetzt automatisch im [!UICONTROL Analytics for Target] Integration (A4T). Der clientseitige Workaround wurde entfernt. (TNT-30247)
* Das clientseitige Edge-Routing ist jetzt standardmäßig aktiviert. (TNT-30261)
* Es wurde ein Problem mit dem Rendering von VEC-Aktionen (Visual Experience Composer) behoben, das bei Abhängigkeiten zwischen den Aktionen auftrat. (TNT-30248)

## „at.js“-Version 1.5.0

at.js Version 1.5.0 ist verfügbar.

* Die Details des Ereignisses `at-request-succeeded` enthalten das Umleitungs-Flag. Mit diesem Flag lässt sich bestimmen, ob die Seite an eine andere URL umgeleitet wird. Die URL können Sie über `at-content-rendering-redirect` ermitteln. (TNT-29834)
* Es wurde ein Problem behoben, bei dem `window.targetGlobalSettings.enabled` mit einem Laufzeitfehler fehlschlug, wenn es auf „false“ festgelegt war. (TNT-29829)
* Es wurde ein Problem behoben, bei dem das Laden einer Seite im Visual Experience Composer (VEC) fehlschlug, wenn benutzerspezifischer Code verwendet wurde, um eine globale Mbox-Anfrage auszulösen, und der Body verborgen wurde. (TNT-29795)
* Unterstützung für `screenOrientation`, `devicePixelRatio` und `webGLRenderer` wurde hinzugefügt. Diese neuen [!DNL Target] -Anfrageparameter werden für die iPhone X- und andere moderne Geräteerkennung verwendet. Weitere Informationen finden Sie unter [Mobilgeräte](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html). (TNT-29781)
* Es wurde ein Problem behoben, bei dem der Hinweis zum AAM-Standort (Adobe Audience Manager) nicht immer gesendet wurde. (TNT-29695)
* Bei Browsern, die diese Funktion unterstützen, wechselt at.js 1.5.0 für den Selektorabruf zu MutationObserver. Versionen vor at.js 1.0.0 nutzten einen MutationObserver-Polyfill, der sich als problematisch erwies. Um die Polyfill-Probleme zu vermeiden, verwendet Version 1.5.0 folgenden Pseudocode, um zu entscheiden, welcher Planungsmechanismus verwendet wird:

  ```
  if MutationObserver is supported
    scheduler = MutationObserver
  else if document is visible
    scheduler = requestAnimationFrame
  else
    scheduler = setTimeout
  ```

## „at.js“-Version 1.3.0

at.js Version 1.3.0 ist verfügbar.

* Die folgenden neuen Ereignisse stehen für die Ablaufverfolgungs-, Debugging- und Anpassungsinteraktionen mit at.js zur Verfügung:

   * LIBRARY_LOADED
   * REQUEST_START
   * CONTENT_RENDERING_START
   * CONTENT_RENDERING_NO_OFFERS
   * CONTENT_RENDERING_REDIRECT

  Weitere Informationen finden Sie unter [at.js – benutzerdefinierte Ereignisse](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md).

* Sie können eine at.js-Anfrage um zusätzliche Parameter erweitern, die von Datenanbietern stammen. Datenanbieter sollten zu `window.targetGlobalSettings` unter `dataProviders key` hinzugefügt werden.

  Weitere Informationen finden Sie unter [Datenanbieter](atjs-functions/targetglobalsettings.md#data-providers).

* at.js-Anfragen verwenden nun GET. Sie wechseln jedoch zu POST, wenn die URL-Größe 2048 Zeichen überschreitet. Es gibt eine neue Eigenschaft mit dem Namen `urlSizeLimit`, wo Sie die Größenbeschränkung bei Bedarf erhöhen können. Diese Änderung ermöglicht [!DNL Target] um at.js an AppMeasurement auszurichten, wobei dieselbe Technik verwendet wird.
* [!DNL Target] erzwingt jetzt, dass der `mbox`-Schlüssel in der `adobe.target.applyOffer(options)`-Funktion verwendet wird. Dieser Schlüssel war in der Vergangenheit erforderlich, aber [!DNL Target] erzwingt nun seine Verwendung, um sicherzustellen, dass [!DNL Target] hat eine ordnungsgemäße Validierung und Kunden verwenden die Funktion ordnungsgemäß.
* at.js weist eine verbesserte Ereignis- und Klick-Tracking-Funktionalität auf. at.js verwendet `navigator.sendBeacon()` zum Senden von Ereignis-Tracking-Daten und weicht zur synchronen XHR aus, wenn `navigator.sendBeacon()` nicht unterstützt wird. Dies wirkt sich hauptsächlich auf Internet Explorer 10 und 11 und einige Safari-Versionen aus. Safari unterstützt `navigator.sendBeacon()` ab der kommenden iOS 11.3-Version.
* at.js kann Angebote nun sogar dann darstellen, wenn eine Seite auf Registerkarten im Hintergrund geöffnet wird. Einige [!DNL Target] Kunden haben beim `requestAnimationFrame()` wurde aufgrund des Browserdrosselungsverhaltens für Hintergrundregisterkarten deaktiviert.
* Diese Version beinhaltet viele Leistungsverbesserungen, einschließlich kürzerer Callstacks, wenn ein Chrome-CPU-Profil untersucht wird.
* at.js 1.3.0 unterstützt die Bereitstellung von Inhalten in Microsoft Internet Explorer 9 nicht mehr. Eine Liste der unterstützten Browser finden Sie unter [Unterstützte Browser](/help/dev/before-implement/supported-browsers.md). Von jetzt an werden alle Anfragen über `XMLHttpRequest` mit CORS-Unterstützung ohne JSONP-Anfragen ausgeführt. Durch diese Änderung wird die Sicherheit erheblich verbessert.

## „at.js“-Version 1.2.3

at.js Version 1.2.3 ist verfügbar.

* Fügt Unterstützung für JSON-Angebote hinzu. JSON-Angebote werden nur bei Aktivitäten unterstützt, die mit dem formularbasierten Experience Composer erstellt wurden. Die einzige Möglichkeit, JSON-Angebote zu nutzen, läuft derzeit über direkte API-Aufrufe. Weitere Informationen finden Sie unter [Erstellen von JSON-Angeboten](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html).

## „at.js“-Version 1.2.2

at.js Version 1.2.2 ist verfügbar.

* Es wurde ein Problem behoben, bei dem ein JavaScript-Fehler zurückgegeben wurde, wenn die Variable [!DNL Target] -Bibliothek, die auf einer Seite im QUIRKS-Modus geladen wird. (TNT-28312)
* Es wurde ein Problem behoben, das [!DNL Target] Klick-Tracking zum Umbruch [!DNL Analytics] Datenerfassungs-Aufrufe. (TNT-28261)
* Es wurde ein Problem behoben, das dazu führte, dass `getOffer() params` fehlschlug, wenn `targetPageParams()` eine leere Zeichenfolge zurückgab. (TNT-28359)
* Es wurde ein Problem mit der Generierung von Sitzungs-IDs bei der Verwendung von x-only behoben. (TNT-28361)

## „at.js“-Version 1.2.1

at.js Version 1.2.1 ist verfügbar.

* Es wurde ein Problem behoben, das beim Klick-Tracking auf einen Link mit target=&quot;_blank&quot; verhindert wurde [!DNL Target] durch Öffnen des Links in einer neuen Registerkarte.

## „at.js“-Version 1.2.0

at.js-Version 1.2 ist nun als Wartungsversion verfügbar, die größtenteils Fehlerkorrekturen enthält.

* Es wurde ein Problem behoben, das Standardaktionen zum Verfolgen von Sonderfällen per Klick verhindert hat. (TNT-28089)
* Es wurde ein Problem beim Klick-Tracking auf einen Link mit `target="_blank"` behoben, das das Öffnen des Links auf einer neuen Registerkarte in verhindert hat. [!DNL Target] (TNT-28072)
* IP-Adressen können als Cookie-Domäne verwendet werden. (TNT-28002)
* Es wurde ein Problem behoben, das in Weiterleitungsangeboten mit einer globalen Mbox oder anderen regionalen Mboxes ein Flackern verursacht hat. (TNT-27978)
* Es wurde ein Problem in [!UICONTROL Erlebnis-Targeting] Die Aktivitätseinrichtung schlägt im VEC beim Wechsel zwischen Durchsuchen und Erstellen fehl. (TNT-27942)
* Es wurde eine falsche Behandlung der Flackerstilklassen für klickbasierte Verfolgungselemente behoben. (TNT-27896)
* Es wurde ein Problem behoben, durch das globale Mbox-Parameter mit allen Mbox-Parametern gemischt wurden. (TNT-27846)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass Handlebars, Mustache und andere Client-seitige Vorlagenbibliotheken von at.js ordnungsgemäß verarbeitet werden. (TNT-27831)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass `sdidParamExpiry` ordnungsgemäß initialisiert und an die Besucher-API übergeben wird. Dies ist eine Regression, die `at.js 1.1.0` hinzugefügt wurde. Vorherige at.js-Versionen sind nicht betroffen. Dies betrifft nur Clients, die Weiterleitungsangebote und A4T verwenden. (TNT-27791)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass `SCRIPT` unabhängig vom verwendeten Typattribut ausgeführt wird. (TNT-27865)

## „at.js“-Version 1.1.0

**Datum:** 2. August 2017

Folgende Verbesserungen und Fehlerbehebungen sind in Version 1.1 von at.js enthalten:

* Die Verarbeitung von Antwort-Token wurde hinzugefügt. Weitere Informationen finden Sie unter [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).
* Es wurde ein Problem behoben, damit `document.currentScript polyfill` nicht mit Angular 1.X in Konflikt gerät.
* Es wurden Änderungen vorgenommen, die sicherstellen, dass die Klick-Verfolgung nicht mit der Sichtbarkeitseigenschaft in Konflikt gerät. Klick-Verfolgungselemente sind mit der CSS-Klasse `at-element-click-tracking` statt mit `at-element-marker` markiert.

## „at.js“-Version 1.0.0

**Datum:** 7. Juli 2017

Folgende Verbesserungen und Fehlerbehebungen sind Version 1.0 von at.js enthalten:

* Unterstützung des asynchronen Ladens von at.js zum schnelleren Laden der Seite.
* Unterstützung zum Ausblenden von Seiteninhalten im Voraus, wenn at.js asynchron geladen wird.
* Bessere Fehlermeldungen bei deaktivierter Inhaltsbereitstellung.
* Leistungsoptimierungen beim Bereitstellen mehrerer Aktivitäten.
* Unterstützung der YUI-Komprimierung.
* Bug/Fehler-Berichterstellung für benutzerdefinierte Ereignisse während der Bereitstellung von Aktivitäten.
* Behebung von Leistungsproblemen in Microsoft Internet Explorer 11.
* Korrektur eines Fehlers der `getOffer()`-Funktion auf einigen Websites.
* Laden Sie die [!DNL Target] -Bibliothek asynchron. Weitere Informationen finden Sie in den [häufig gestellten Fragen zu „at.js“](/help/dev/implement/client-side/atjs/target-atjs-faq.md).

## „at.js“-Version 0.9.7

**Datum:** 22. Mai 2017

Folgende Verbesserungen und Fehlerbehebungen sind in Version 0.9.7 von at.js enthalten:

* Es wurde ein Problem bezüglich eines Asset-Schlüssels behoben, der in den Aktionen `insertAfter` und `insertBefore` im Visual Experience Composer (VEC) gefehlt hat. Diese Probleme bezogen sich auf die Migration von visuellen Angeboten zu Angebotsvorlagen.

## „at.js“-Version 0.9.6

**Datum:** 13. April 2017

Folgende Verbesserungen und Fehlerbehebungen sind in Version 0.9.6 von at.js enthalten:

* Unterstützung für Umleitungsangebote für A4T. Nachdem Sie Version 0.9.6 von at.js heruntergeladen haben, können Sie Umleitungsangebote in Aktivitäten verwenden, die [!UICONTROL Adobe Analytics als Berichtsquelle für Target] (A4T) nutzen. Neben Version 0.9.6 von at.js bestehen weitere Mindestanforderungen für Ihre Implementierung, um Umleitungsangebote und A4T nutzen zu können. Weitere wichtige Informationen finden Sie unter [Umleitungsangebote – A4T-FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html).
* Vor at.js 0.9.6, wenn die Besucher-API auf der Seite vorhanden war und die `visitorApiTimeout` Einstellung war zu aggressiv. [!DNL Target] konnte in eine Situation geraten, in der keine MCID-Daten in der [!DNL Target] -Anfrage. So konnte es bei der Verwendung von A4T zu Problemen wie z. B. aufgetrennten Treffern in [!DNL Analytics] kommen.

  Dieses Verhalten wurde in at.js 0.9.6 geändert, auch wenn die `visitorApiTimeout` auf &quot;1 ms&quot;eingestellt ist, [!DNL Target] versucht, Daten zu SDID, Tracking-Servern und Kunden-IDs zu erfassen und diese in der [!DNL Target] -Anfrage.

* Die Einstellung `selectorsPollingTimeout` wurde hinzugefügt. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Das Antwortformat von `getOffer()` wurde geändert. Weitere Informationen finden Sie unter [adobe.target.getOffer(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md).
* Die Konsolenprotokollierung für nicht unterstützte `<!DOCTYPE>`-Deklarationen wurde hinzugefügt.
* Es wurde ein Problem behoben, bei dem [!DNL Target Classic] -Plug-ins nicht korrekt angewendet wurden, wenn mehrere Standardangebote an eine Mbox gesendet wurden. (TGT-22664)
* Die Cookie-Einstellung für Domänen auf oberster Ebene mit zwei Buchstaben wurde verbessert, um zu gewährleisten, dass das Mbox-Cookie für entsprechende Domänen korrekt festgelegt wird (z. B. test.no, autodrives.ca usw.).
* Der Algorithmus zum Extrahieren der Domain der obersten Ebene, die beim Speichern von Cookies verwendet werden sollte, hat sich in at.js-Version 0.9.6 geändert. Aufgrund dieser Änderung können keine Cookies für Adressen gespeichert werden, die IP verwenden. IP-Adressen werden größtenteils zu Testzwecken verwendet. Als Problemumgehung können Sie jedoch DNS-Einträge verwenden oder die Hosts-Datei auf einer lokalen Box anpassen.
* Die Verarbeitung von Aktionen zum Verschieben und Neuanordnen bei Zeichenfolgenwerten anstelle von Ganzzahlen als Eigenschaften wurde korrigiert.

## „at.js“-Version 0.9.4

**Datum:** 19. Januar 2017

* Mbox-Namen können jetzt Sonderzeichen wie das kaufmännische Und (&amp;) enthalten. 

  Eine Liste der zulässigen Sonderzeichen finden Sie unter [&quot;at.js&quot;-Konfiguration](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

* Die Funktion `secureOnly` wurde hinzugefügt, die anzeigt, ob at.js nur HTTPS verwenden soll oder ob es möglich ist, dass basierend auf dem Seitenprotokoll zwischen HTTP und HTTPS umgeschaltet wird. Es handelt sich hierbei um eine erweiterte Einstellung, deren Standardwert „false“ (falsch) lautet und die von `targetGlobalSettings` überschrieben werden kann.
* Die Option Unterstützung älterer Browser ist in at.js, Version 0.9.3 und älter verfügbar. Diese Option wurde in at.js, Version 0.9.4 entfernt.

## „at.js“-Version 0.9.3

**Datum:** 10. Oktober 2016

* Stellt sicher, dass Mbox-Aufrufe in Microsoft Internet Explorer 11 ausgelöst werden, wenn veraltete Browser in den at.js-Einstellungen deaktiviert sind.
* Stellt sicher, dass Standardinhalte wiedergegeben werden, wenn ein dynamisches Remote-Angebot fehlschlägt (wenn beispielsweise die URL nicht korrekt ist und eine 404-Fehlermeldung angezeigt wird).
* Stellt sicher, dass Elemente schnell angezeigt werden, wenn im DOM keine Selektoren für VEC-Clicktracking gefunden werden.

## „at.js“-Version 0.9.2

**Datum:** 21. September 2016

* Es wurde die Einstellung `optoutEnabled` hinzugefügt, um die Abmeldung für Gerätediagramme zu ermöglichen. Ist diese Option als `true` eingestellt und hat sich der Besucher gegen eine Verfolgung entschieden, ruft der Browser des Benutzers die Mbox nicht auf. Gerätediagramme sind derzeit als Betaversion verfügbar. Diese Einstellung ist standardmäßig als `false` festgelegt, muss allerdings in `true` geändert werden, wenn Sie Gerätediagramme nutzen.
* Erweiterte Unterstützung für `CustomEvent` im Benachrichtigungsmechanismus. In der Vergangenheit konnte der Ereignis-Benachrichtigungsmechanismus von at.js nicht mit Standard-DOM-APIs wie `document.addEventListener()` () verwendet werden. Jetzt können Sie `document.addEventListener()` verwenden, um at.js-Ereignisse, z. B. Abfrage- und Inhaltswiedergabe-Ereignisse, zu abonnieren.
* Es wurde ein Problem im Zusammenhang mit Angeboten behoben, die im Visual Experience Composer (VEC) erstellt wurden. Vor dieser Version [!DNL Target] die Selektoren ausgeblendet und sie nur dann wieder eingeblendet, wenn alle Selektoren übereinstimmen. In at.js 0.9.2 [!DNL Target] Blendet die Selektoren ein, sobald sie übereinstimmen.

## „at.js“-Version 0.9.1

**Datum:** 14. Juli 2016

* Stellt für at.js eine Zeitüberschreitung für den Besucher-ID-Dienst bereit, die unabhängig von der Zeitüberschreitung des Diensts ist.
* Behebung eines Problems in Version 0.9.0, das sich auf Implementierungen mit at.js auf einigen Seiten und mbox.js (jetzt nicht mehr unterstützt) auf anderen Seiten auswirkte.
* Wenn Sie [!DNL Adobe Analytics] als Berichtsquelle für Ihre Aktivität verwenden, müssen Sie bei der Erstellung einer Aktivität keinen Trackingserver angeben, wenn Sie mbox.js , Version 61 (oder neuer) oder at.js , Version 0.9.1 (oder neuer) verwenden. Die at.js-Bibliothek sendet automatisch Tracking-Server-Werte an [!DNL Target]. Bei der Erstellung einer Aktivität können Sie das Feld Tracking Server auf der Seite Ziele und Einstellungen leer lassen.

## „at.js“-Version 0.9.0

**[!DNL Target]Version:** 16.6.1

**Datum:** 23. Juni 2016

* Behebung eines Whitescreen-Problems bei der Verwendung von VEC-Angeboten. Jeder, der at.js verwendet, sollte auf diese neue Version aktualisieren.
* Neue `registerExtension`-API.

  Mit dieser neuen API erhalten Entwickler Zugriff auf bestimmte jQuery-Module, die in at.js zur Entwicklung von Erweiterungen (Plugins) für die Bibliothek verwendet werden. Für diese Änderung gibt es verschiedene Gründe. Die Änderung wirkt sich nur auf Benutzer aus, die mit folgenden Funktionen arbeiten:

   * Die `getSettings()`-API wurde entfernt, die gleichen Funktionen sind aber über `registerExtension()` verfügbar.
   * Die `getTracking()`-API wurde entfernt, die gleichen Funktionen sind aber über `registerExtension()` verfügbar.

   * Bestehende Erweiterungen (z. B. Erweiterungen für AngularJS) müssen aktualisiert werden, damit `registerExtension()` verwendet werden kann.

* Neue at.js-Benachrichtigungs-API.

  Ziel dieses Benachrichtigungssystems ist es, bessere Einsichten in at.js und die zugehörigen Aktivitäten auf der Seite zu ermöglichen sowie aufzuzeigen, wenn Fehler auftreten. Ein häufig im VEC auftretendes Problem ist, dass sich bei einem IT-Release die Seite ändert. Somit wird ein VEC-Selektor beschädigt und der Test kann Inhalte nicht mehr ordnungsgemäß bereitstellen. Ziel dieses Benachrichtigungssystems ist es, die Seite auf dieses Bereitstellungsproblem aufmerksam zu machen, sodass Entwickler auf die Informationen zugreifen, sie an ein System wie [!DNL Adobe Analytics] weiterleiten und Nachrichten an den Geschäftsinhaber übermitteln können, um darüber zu informieren, dass der Test nicht mehr funktioniert.

* Neue `targetGlobalSettings()`-API-Methode.

  Sie können Einstellungen in der at.js-Bibliothek überschreiben, anstatt sie in der [!DNL Target Standard/Premium] Benutzeroberfläche oder durch Verwendung von REST-APIs.

## „at.js“-Version 0.8.0

**Datum:** 5. Mai 2016.

Dies ist die erste offizielle Version der „at.js“-Bibliothek.

at.js ist die neue Implementierungsbibliothek für [!DNL Target] und ist sowohl auf typische Webimplementierungen als auch auf Einzelseitenanwendungen ausgelegt.

at.js ersetzt mbox.js für [!DNL Adobe Target]-Implementierungen.

Neben anderen Vorteilen sorgt at.js für kürzere Ladezeiten von Seiten bei Webimplementierungen, erhöhte Sicherheit und bessere Implementierungsoptionen für Einzelseitenanwendungen.

„at.js “ enthält die Komponenten, die sich in „target.js“ befanden, weshalb kein Aufruf mehr an „target.js“ erfolgt.

Achten Sie bei der Implementierung von „at.js“ auf Folgendes:

* Versionen von Internet Explorer, die älter als Version 8 sind, werden nicht unterstützt.
* Aufgrund der asynchronen Implementierung funktionieren ältere Integrationen, wie das Plugin von [!UICONTROL Test&amp;Target zu SiteCatalyst], möglicherweise nicht mehr.
* [!DNL Target]-Plug-ins, die mbox.js-Objekte und -Methoden referenzieren, werden nicht unterstützt.
* Alle [!DNL Target]-Aufrufe werden über XMLHTTPRequest getätigt und Inhalt wird über JSON zurückgegeben.
