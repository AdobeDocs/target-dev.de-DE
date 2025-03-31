---
keywords: at.js-Versionen, at.js-Versionen, Versionshinweise
description: Zeigen Sie die Details der Änderungen in den einzelnen Versionen der  [!DNL Adobe Target] .js-JavaScript-Bibliothek an.
title: Was ist in jeder Version von at.js enthalten?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: aa6f6593a6979666101d8754dde3e02fb6a21e33
workflow-type: tm+mt
source-wordcount: '5018'
ht-degree: 64%

---

# „at.js“-Versionsdetails

Details zu den Änderungen in den einzelnen Versionen der at.js-JavaScript-Bibliothek von [!DNL Adobe Target]

>[!IMPORTANT]
>
>[!DNL Adobe Target] unterstützt sowohl at.js 1.*x* und in at.js 2.*x*.
>
>at.js 1.*x* wurde in den Wartungsmodus versetzt. Das [!DNL Target]-Team veröffentlicht bei Bedarf Fehlerbehebungen und Sicherheits-Patches.
>
>Das [!DNL Target]-Team bietet vollständige Unterstützung für at.js 2.*x* und veröffentlicht laufend Fehlerbehebungen, Sicherheits-Patches, Funktionen und Leistungsoptimierung.
>
>Sie sollten auf die neuesten Versionen von entweder 1 aktualisieren.*x* oder 2 *x*, um Fehlerbehebungen und Sicherheitspatches für Probleme zu erhalten, die in einer früheren Nebenversion der entsprechenden Hauptversion entdeckt wurden.

Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sind die bevorzugte Methode zum Aktualisieren von at.js. Erweiterungsentwickler fügen ihren Erweiterungen kontinuierlich neue Funktionen hinzu und beheben häufig Fehler. Diese Aktualisierungen werden in neue Versionen einer Erweiterung gepackt und im Adobe Experience Platform-Katalog als Aktualisierungen verfügbar gemacht. Weitere Informationen finden Sie unter [Erweiterungs-Upgrades](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html) im Handbuch *Übersicht über Tags*.

## at.js-Version 2.11.8 (31. März 2025)

* Behobene CodeQL-identifizierte Sicherheitslücke in der Validierung von Zeichenfolgen-Suffixen, um Edge-Fälle während Größenänderungs- und Verschiebungsvorgängen zu verhindern. (TNT-51516)

## at.js-Version 2.11.7 (26. Februar 2025)

* Fehlerkorrektur - Die Telemetrie-Protokollierung funktioniert jetzt, wenn `localStorage` nicht verfügbar ist. Die Telemetrie verursachte bei einigen Kunden, die in ihren Browsern deaktiviert `localStorage`, ein Problem.

## at.js-Version 2.11.6 (29. September 2024)

* Es wurde ein Problem behoben, das dazu führte, dass [!DNL Target] mit Umleitungsangeboten innerhalb des [!UICONTROL Visual Experience Composer] (VEC) oder [!UICONTROL Form-Based Experience Composer] nicht ordnungsgemäß funktionierten.

## at.js-Version 2.11.5 (14. August 2024)

* Es wurde eine Zwischenspeicherung für Lese- und Schreibvorgänge von Cookies implementiert, um den Mehraufwand für das wiederholte, kostspielige Parsen und Bearbeiten von Zeichenfolgen zu reduzieren.
* Die neuere URL Search Params-API wurde implementiert, sofern verfügbar, da sie schneller ist als das manuelle Parsen und Bearbeiten von Zeichenfolgen.

## at.js-Version 2.11.4 (Donnerstag, 24. Januar 2024)

* at.js wurde aktualisiert, um zu verhindern, dass ungültige Geodaten an die Bereitstellungs-API gesendet werden.

## at.js-Version 2.11.3 (21. November 2023)

* Fehlerkorrektur - Antwort-Token werden jetzt bei `at-content-rendering-failed` Ereignissen gesendet.

## at.js-Version 2.11.2 (Freitag, 26. Oktober 2023)

* Es wurde ein Problem behoben, das zu Inkonsistenzen in Antwort-Token führte, die bei benutzerdefinierten Ereignissen gesendet wurden.

## at.js-Version 2.11.1 (Samstag, 13. Oktober 2023)

* Es wurde ein Problem behoben, das zu nicht abgefangenen Fehlern führte, während sich eine Seite, auf der at.js ausgeführt wurde, im Quirks-Modus befand.

## at.js-Version 2.11.0 (Mittwoch, 10. Oktober 2023)

* Es wurde Unterstützung für das Festlegen benutzerdefinierter [!DNL Adobe Experience Platform] (AEP)-`sandboxId` und -`sandboxName` in `targetGlobalSettings` hinzugefügt, die bei `getOffer/getOffers`-Aufrufen an die Bereitstellungs-API übergeben werden.
* Schatten-DOM-Fehlerbehebung für die Verkettung von `:eq()` in Selektoren.

## at.js-Version 2.10.3 (12. September 2023)

* Es wurde ein Problem behoben, das fälschlicherweise das `at-content-rendering-succeeded` benutzerspezifische Ereignis auslöste, wenn keine Angebote gerendert wurden. Das richtige Ereignis `at-content-rendering-no-offers` wird jetzt ausgelöst.
* `eventToken` und `responseTokens` wurden zum Fehlerobjekt für das benutzerdefinierte `at-content-rendering-failed`-Ereignis hinzugefügt.

## at.js-Version 2.10.2 (7. März 2023)

* Es wurde ein Fehler behoben, der dazu geführt hatte, dass die Funktion `trackEvent` immer einen Fehler zurückgab.

## at.js-Version 2.10.1 (2. Februar 2023)

* Es wurde ein Fehler behoben, durch den Aktivitäten in Verbindung mit Zielgruppenregeln, die Parameter mit Punkten in ihren Namen enthielten, beim On-Device Decisioning nicht das erwartete Erlebnis zurückgaben.
* Es wurde ein in at.js 2.6.0 eingeführter Fehler behoben, durch den at.js einen Bereitstellungsaufruf auslöste, selbst wenn mboxDisable aktiviert war.

## at.js-Version 2.10.0 (Dienstag, 19. September 2022)

* Unterstützung von Drittanbieter-Cookies hinzugefügt.

## at.js-Version 2.9.0 (27. Mai 2022)

* Unterstützung für [User Agent Client Hints](user-agent-and-client-hints.md) wurde hinzugefügt.
* Es wurde ein Fehler behoben, durch den mehrere Mbox-Anfragen auf derselben Seite unterschiedliche Impressions-IDs erhielten.

## at.js-Version 2.8.1 (28. Januar 2022)

* Es wurde ein Problem behoben, `pageLoad` im hybriden Ausführungsmodus On Device Decisioning (ODD) nicht auf target-global-mbox abgebildet wurde.
* Es wurde ein Problem mit Analysedetails für mbox-Anfragen behoben.
* Dev-Abhängigkeiten wurden aktualisiert, um Sicherheitslücken zu beheben.

## at.js-Version 2.8.0 (7. Januar 2022)

Die at.js-JavaScript-Bibliothek von [!DNL Target] erfasst jetzt Daten zur Nutzung von Funktionen und Daten der Leistungsmessung. Personenbezogene Daten werden nicht erfasst. Eine Abwahl dieser Funktion ist verfügbar, indem `telemetryEnabled` in `targetGlobalSettings` auf „false“ gesetzt wird. Weitere Informationen finden Sie unter [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled).

## at.js-Version 2.7.0 (28. Oktober 2021)

Diese Version enthält die folgende Verbesserung:

* Hinzugefügte Unterstützung für [Web-Komponenten](https://developer.mozilla.org/de/docs/Web/Web_Components). Diese Version von at.js ist erforderlich, um personalisierte Erlebnisse und Angebote für benutzerdefinierte Elemente und Elemente innerhalb von benutzerdefinierten Elementen zu erstellen und zu testen. Diese Funktion ist in der Version 21.10.5 von [!DNL Target Standard/Premium] enthalten.

## at.js 1.8.3 (21. September 2021)

Diese Version enthält die folgenden Änderungen:

* Die `reactor-window` und `reactor-document` Adobe Experience Platform Launch-Module wurden entfernt, um sicherzustellen, dass der Platform Launch-Build für Kunden, die `window.default` oder `document-default` festgelegt haben, ordnungsgemäß funktioniert.
* at.js 1.8.3 legt jetzt explizit `Samesite=None` und `Secure` fest, um sicherzustellen, dass Domain-Cookies von Drittanbietern ordnungsgemäß gesetzt werden.

## at.js 2.6.1 (16. August 2021)

* Fehlerbehebung für „Für den Hybrid-Modus ist kein zwischengespeichertes Artefakt verfügbar“ bei Verwendung der geräteinternen Entscheidungsfindung.

## at.js 2.6.0 (16. Juli 2021)

* Das Attribut „secure“ wurde zu Cookies hinzugefügt für alle Fälle, in denen die at.js-Einstellungen `secureOnly` auf `true` gesetzt sind.
* Bei Verwendung von `triggerView()` sind jetzt Antwort-Token verfügbar.
* Es wurde ein Problem im Zusammenhang mit dem Ereignis `CONTENT_RENDERING_NO_OFFERS` behoben. Jetzt wird dieses Ereignis korrekt ausgelöst, wenn kein Inhalt von [!DNL Target] zurückgegeben wird.
* Details zur Klickmetrik von [!UICONTROL Analytics for Target] (A4T) werden bei der Verwendung von `prefetch`-Anfragen korrekt zurückgegeben.
* Die UUID-Generierung verwendet nicht mehr `Math.random()`, sondern beruht auf `window.crypto`.
* Der Ablauf des `sessionId`-Cookies wird bei jedem Netzwerkaufruf korrekt verlängert.
* Die Ansichts-Cache-Initialisierung für die Einzelseiten-Anwendung (SPA, Single Page Application) wird jetzt korrekt verarbeitet und berücksichtigt `viewsEnabled` Einstellungen. Wenn `viewsEnabled` auf den `false` Wert gesetzt wird, wird die `triggerView()` deaktiviert. Siehe [Reihenfolge der Vorgänge beim ersten Laden der Seite](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order).

## at.js 2.5.0 (13. Mai 2021)

Diese Version von at.js umfasst die folgenden Verbesserungen und Änderungen:

* Unterstützung der [geräteinternen Entscheidungsfindung](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) für at.js.
* Unterstützung für [Vorschau-Links](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) für Automated Personalization-Aktivitäten

Mit dieser Version endet auch die Unterstützung für Microsoft Internet Explorer 10 und höher.

## at.js 2.4.1 (23. März 2021)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Es wurde ein Problem behoben, bei dem `targetPageParams` in Mbox-Anfragen enthalten waren. `targetPageParams` sollten nur in `pageLoad`-Anfragen enthalten sein. (TNT-40247)
* Optimierte globale Fenster- und Dokumentreferenzen in der Adobe Experience Platform-Erweiterung. (TNT-37124)

## at.js 2.4.0 (14. Januar 2021)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Fehlerbehebungen enthält:

* Unterstützt einheitliche Profil-/Plattform-ID für Bereitstellungs-API-Kunden-IDs.
* Die fehlerhafte Style-Tag-Injektion wurde behoben.

## at.js 2.3.3 (13. November 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgende Fehlerbehebung enthält:

* Es wurde ein Problem im Zusammenhang mit Mbox-Klick-Tracking und A4T behoben. Mit 0n-Klick löste [!DNL Target] einen Bereitstellungs-API-Aufruf mit den richtigen Mbox- und Mbox-Parametern aus. Die SDID stimmte jedoch nicht mit der im [!DNL Analytics]-Aufruf überein, daher gab es keine Trefferzuordnung und Konversion. (TNT-38372)

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
* Fehlerkorrektur - Bei der Verwendung von [!DNL Target] Extension v2 und der [!UICONTROL Adobe Analytics Launch]-Erweiterung wird der [!DNL Analytics] `sendBeacon`-Aufruf [!DNL Target] verzögert. (TNT-36407, TNT-35990, TNT-36000)

## at.js-Version 2.3.0 (Donnerstag, 25. März 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Unterstützung für das Festlegen von Content Security Policy-Nonces für SCRIPT- und STYLE-Tags, die beim Anwenden bereitgestellter [!DNL Target] an das Seiten-DOM angehängt werden. Kunden können `targetGlobalSettings.cspScriptNonce` und `targetGlobalSettings.cspStyleNonce` festlegen, damit at.js die entsprechenden Skript- und Stil-Tag-Nonces für angewendete Angebote festlegen kann. Siehe [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) für weitere Details.
* Fehlerkorrektur - Beim Kompilieren von at.js mit dem Google Closure-Compiler für die Google Tag Manager-Bereitstellung tritt jetzt kein Fehler mehr auf.
* Das Check-Cookie at.js wurde von `check` in `at_check` umbenannt, um Kollisionen mit den Implementierungen des Kunden zu vermeiden.

## at.js-Version 1.8.1 (Donnerstag, 25. März 2020)

Diese Version von at.js ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

* Das Check-Cookie at.js wurde von `check` in `at_check` umbenannt, um Kollisionen mit den Implementierungen des Kunden zu vermeiden.

## at.js-Version 2.2.0 (Freitag, 10. Oktober 2019)

Diese Version von at.js umfasst die folgenden Verbesserungen und Fehlerbehebungen:

* Es wurde ein Problem behoben, bei dem beim Klick-Tracking keine Konversionen in [!DNL Analytics for Target] (A4T) gemeldet wurden, wenn [!DNL Adobe Analytics] Code nicht in Seitenelementen vorhanden war.
* Verbesserte Leistung bei Verwendung von sowohl Experience Cloud ID Service (ECID) v4.4 als auch at.js 2.2 auf Ihren Web-Seiten.
* Bislang führte ECID zwei Sperraufrufe durch, bevor at.js Erlebnisse abrufen konnte. Dies wurde auf einen Aufruf reduziert, wodurch die Leistung deutlich verbessert wurde.
* Fehlerkorrektur - Bei der Verarbeitung vorab abgerufener Ansichten wurden Ereignis-Token aus Standardangeboten nicht in die gesendeten Benachrichtigungen einbezogen.

>[!NOTE]
>
>Aktualisieren Sie Ihre ECID-Erweiterung auf Version 4.4, um diese Leistungsverbesserung nutzen zu können.

* at.js 2.2 bietet außerdem eine neue Einstellung namens `serverState`. Diese Einstellung kann verwendet werden, um die Seitenleistung zu optimieren, wenn eine Hybrid-Integration von [!DNL Target] implementiert ist. Hybrid-Integration bedeutet, dass Sie zur Bereitstellung Ihrer Erlebnisse sowohl at.js v2.2+ auf der Client-Seite als auch die Bereitstellungs-API oder eine [!DNL Target] SDK auf der Server-Seite verwenden. `serverState` bietet at.js v2.2+ die Möglichkeit, Erlebnisse direkt aus Inhalten anzuwenden, die auf Serverseite abgerufen und als Teil der bereitzustellenden Seite an den Client zurückgegeben wurden. Weitere Informationen finden Sie unter „serverState“ in [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate).

## at.js-Version 1.8.0 (Freitag, 10. Oktober 2019)

Diese Version von at.js umfasst die folgenden Verbesserungen und Fehlerbehebungen:

* Verbesserte Leistung bei Verwendung von sowohl Experience Cloud ID Service (ECID) v4.4 als auch at.js 1.8 auf Ihren Web-Seiten.
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

* **Client-seitige Analytics-Protokollierung**: Geben Sie Kunden die volle Kontrolle darüber, wie sie Analysedaten an [!DNL Adobe Analytics] senden möchten, ob Client- oder Server-seitig.

  Weitere Informationen finden Sie unter [Client-seitig [!DNL Analytics] logging](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side).

* **Benachrichtigungen senden**: Erlauben Entwicklern, Benachrichtigungen zu senden, wenn ein Erlebnis durch ihren Code statt über `applyOffer()` oder `applyOffers()` gerendert wird.

  Weitere Informationen finden Sie unter [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md).

* **at.js-Größe um ~ 24 % verringert**: Die Größe von at.js wurde um ~ 24 % verringert. Die kleinere Dateigröße verbessert die Seitenladeleistung und verringert die Ladedauer von at.js auf der Seite.

## at.js-Version 2.0.1 (19. März 2019)

Dies ist eine Wartungsversion, die die folgenden Erweiterungen und Fehlerbehebungen enthält:

(Die Problemnummern in Klammern dienen internen Adobe-Benutzern.)

* Es wurde eine Race-Bedingung im DOM-Polling-Code behoben, durch die JavaScript-Ausnahmen für bestimmte Kunden verursacht wurden. (TNT-31869)
* Benachrichtigungen, die angezeigt wurden, wurden von Click-Tracking-Ereignishandlern entkoppelt. Zunächst sendeten [!DNL Target] keine Benachrichtigungen, wenn zu einer gerenderten Ansicht gehörende Klick-Ereignis-Handler nicht angehängt werden konnten. [!DNL Target] sendet jetzt eine Ansichtsbenachrichtigung, auch wenn keine Klickelemente gefunden werden. (TNT-31969)
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
>Wenn Sie Opt-in-Unterstützung von Adobe für die [Datenschutz-Grundverordnung](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) (DSGVO) benötigen, müssen Sie derzeit at.js 1.7.0 oder at.js 2.1.0 oder höher verwenden.

## „at.js“-Version 1.7.0

at.js 1.7.0 bietet Adobe Opt-in-Unterstützung. Adobe Opt-In bietet die Möglichkeit, Adobe-Lösungsintegrationen mit Genehmigungsverwaltungsplattformen zu vereinfachen.

Weitere Informationen zu Adobe Opt-in finden Sie unter [Privatsphäre und Datenschutz-Grundverordnung (DSGVO)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

In dieser Version wird auch ein Problem behoben, bei dem [!DNL Target] Umleitungs-URL-Parameter mit Parametern überschreiben können, die von der Umleitungs-URL stammen.

>[!NOTE]
>
>Wenn Sie für die DSGVO Opt-in-Unterstützung von Adobe benötigen, müssen Sie derzeit at.js 1.7.0 oder at.js 2.1.0 oder höher verwenden.

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
* Es wurde ein Problem behoben, durch das bei Verwendung von [!DNL Analytics for Target] (A4T) anscheinend nicht alle Erlebnisse mit Umleitungen bereitgestellt wurden. (TNT-30444)
* Es wurde ein Problem behoben, das dazu führte, dass die Seite ausgeblendet wurde, nachdem der [!DNL Target]-Aufruf erfolgreich war. (TNT-30358)

Im Folgenden finden Sie einige Verbesserungen und Fehlerbehebungen in „at.js“-Version 1.6.0:

* Umleitungsangebote werden jetzt automatisch in der [!UICONTROL Analytics for Target] (A4T)-Integration unterstützt. Der clientseitige Workaround wurde entfernt. (TNT-30247)
* Das clientseitige Edge-Routing ist jetzt standardmäßig aktiviert. (TNT-30261)
* Es wurde ein Problem mit dem Rendering von VEC-Aktionen (Visual Experience Composer) behoben, das bei Abhängigkeiten zwischen den Aktionen auftrat. (TNT-30248)

## „at.js“-Version 1.5.0

at.js Version 1.5.0 ist verfügbar.

* Die Details des Ereignisses `at-request-succeeded` enthalten das Umleitungs-Flag. Mit diesem Flag lässt sich bestimmen, ob die Seite an eine andere URL umgeleitet wird. Die URL können Sie über `at-content-rendering-redirect` ermitteln. (TNT-29834)
* Es wurde ein Problem behoben, bei dem `window.targetGlobalSettings.enabled` mit einem Laufzeitfehler fehlschlug, wenn es auf „false“ festgelegt war. (TNT-29829)
* Es wurde ein Problem behoben, bei dem das Laden einer Seite im Visual Experience Composer (VEC) fehlschlug, wenn benutzerspezifischer Code verwendet wurde, um eine globale Mbox-Anfrage auszulösen, und der Body verborgen wurde. (TNT-29795)
* Unterstützung für `screenOrientation`, `devicePixelRatio` und `webGLRenderer` wurde hinzugefügt. Diese neuen [!DNL Target]-Anforderungsparameter werden für die iPhone X- und andere moderne Geräteerkennung verwendet. Weitere Informationen finden Sie unter [Mobilgeräte](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html). (TNT-29781)
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

* at.js-Anfragen verwenden nun GET. Sie wechseln jedoch zu POST, wenn die URL-Größe 2048 Zeichen überschreitet. Es gibt eine neue Eigenschaft mit dem Namen `urlSizeLimit`, wo Sie die Größenbeschränkung bei Bedarf erhöhen können. Durch diese Änderung können [!DNL Target] at.js an AppMeasurement ausrichten, das dieselbe Technik verwendet.
* [!DNL Target] erzwingt jetzt, dass der `mbox` in der `adobe.target.applyOffer(options)` verwendet wird. Dieser Schlüssel war in der Vergangenheit erforderlich, erzwingt [!DNL Target] jetzt jedoch seine Verwendung, um sicherzustellen, dass [!DNL Target] ordnungsgemäß validiert wurde und Kundinnen und Kunden die Funktion ordnungsgemäß verwenden.
* at.js weist eine verbesserte Ereignis- und Klick-Tracking-Funktionalität auf. at.js verwendet `navigator.sendBeacon()` zum Senden von Ereignis-Tracking-Daten und weicht zur synchronen XHR aus, wenn `navigator.sendBeacon()` nicht unterstützt wird. Dies wirkt sich hauptsächlich auf Internet Explorer 10 und 11 und einige Safari-Versionen aus. Safari unterstützt `navigator.sendBeacon()` ab der kommenden iOS 11.3-Version.
* at.js kann Angebote nun sogar dann darstellen, wenn eine Seite auf Registerkarten im Hintergrund geöffnet wird. Bei einigen [!DNL Target]-Kunden trat ein Problem auf, wenn `requestAnimationFrame()` aufgrund des Browser-Drosselungsverhaltens für Hintergrund-Registerkarten deaktiviert wurde.
* Diese Version beinhaltet viele Leistungsverbesserungen, einschließlich kürzerer Callstacks, wenn ein Chrome-CPU-Profil untersucht wird.
* at.js 1.3.0 unterstützt die Bereitstellung von Inhalten in Microsoft Internet Explorer 9 nicht mehr. Eine Liste der unterstützten Browser finden Sie unter [Unterstützte Browser](/help/dev/before-implement/supported-browsers.md). Von jetzt an werden alle Anfragen über `XMLHttpRequest` mit CORS-Unterstützung ohne JSONP-Anfragen ausgeführt. Durch diese Änderung wird die Sicherheit erheblich verbessert.

## „at.js“-Version 1.2.3

at.js Version 1.2.3 ist verfügbar.

* Fügt Unterstützung für JSON-Angebote hinzu. JSON-Angebote werden nur bei Aktivitäten unterstützt, die mit dem formularbasierten Experience Composer erstellt wurden. Die einzige Möglichkeit, JSON-Angebote zu nutzen, läuft derzeit über direkte API-Aufrufe. Weitere Informationen finden Sie unter [Erstellen von JSON-Angeboten](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html).

## „at.js“-Version 1.2.2

at.js Version 1.2.2 ist verfügbar.

* Es wurde ein Problem behoben, das einen JavaScript-Fehler zurückgab, wenn die [!DNL Target]-Bibliothek im QUIRKS-Modus auf eine Seite geladen wurde. (TNT-28312)
* Ein Problem wurde behoben, das dazu führte, dass [!DNL Target] Klick-Tracking [!DNL Analytics] Datenerfassungsaufrufe beschädigte. (TNT-28261)
* Es wurde ein Problem behoben, das dazu führte, dass `getOffer() params` fehlschlug, wenn `targetPageParams()` eine leere Zeichenfolge zurückgab. (TNT-28359)
* Es wurde ein Problem mit der Generierung von Sitzungs-IDs bei der Verwendung von x-only behoben. (TNT-28361)

## „at.js“-Version 1.2.1

at.js Version 1.2.1 ist verfügbar.

* Es wurde ein Problem behoben, durch das [!DNL Target] beim Klick-Tracking für einen Link mit target=„_blank“ daran gehindert wurde, den Link in einer neuen Registerkarte zu öffnen.

## „at.js“-Version 1.2.0

at.js Version 1.2 ist jetzt als Wartungsversion verfügbar, die hauptsächlich Fehlerkorrekturen enthält.

* Es wurde ein Problem behoben, das Standardaktionen zum Verfolgen von Sonderfällen per Klick verhindert hat. (TNT-28089)
* Fehlerkorrektur - Beim Klick-Tracking für einen Link mit `target="_blank"` kann der Link jetzt in einer neuen Registerkarte geöffnet [!DNL Target]. (TNT-28072)
* IP-Adressen können als Cookie-Domäne verwendet werden. (TNT-28002)
* Es wurde ein Problem behoben, das in Weiterleitungsangeboten mit einer globalen Mbox oder anderen regionalen Mboxes ein Flackern verursacht hat. (TNT-27978)
* Es wurde ein Problem behoben, bei [!UICONTROL Experience Targeting] die Aktivitätseinrichtung im VEC beim Wechsel zwischen Durchsuchen und Erstellen fehlschlug. (TNT-27942)
* Es wurde eine falsche Behandlung der Flackerstilklassen für klickbasierte Verfolgungselemente behoben. (TNT-27896)
* Es wurde ein Problem behoben, durch das globale Mbox-Parameter mit allen Mbox-Parametern gemischt wurden. (TNT-27846)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass Handlebars, Mustache und andere Client-seitige Vorlagenbibliotheken von at.js ordnungsgemäß verarbeitet werden. (TNT-27831)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass `sdidParamExpiry` ordnungsgemäß initialisiert und an die Besucher-API übergeben wird. Dies ist eine Regression, die `at.js 1.1.0` hinzugefügt wurde. Frühere at.js-Versionen sind davon nicht betroffen. Dies betrifft nur Clients, die Weiterleitungsangebote und A4T verwenden. (TNT-27791)
* Es wurden Änderungen vorgenommen, die sicherstellen, dass `SCRIPT` unabhängig vom verwendeten Typattribut ausgeführt wird. (TNT-27865)

## „at.js“-Version 1.1.0

**Datum:** 2. August 2017

Die folgenden Verbesserungen und Fehlerbehebungen sind in at.js-Version 1.1 enthalten:

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
* [!DNL Target] asynchron laden. Weitere Informationen finden Sie in den [häufig gestellten Fragen zu „at.js“](/help/dev/implement/client-side/atjs/target-atjs-faq.md).

## „at.js“-Version 0.9.7

**Datum:** 22. Mai 2017

Die folgenden Verbesserungen und Fehlerbehebungen sind in at.js-Version 0.9.7 enthalten:

* Es wurde ein Problem bezüglich eines Asset-Schlüssels behoben, der in den Aktionen `insertAfter` und `insertBefore` im Visual Experience Composer (VEC) gefehlt hat. Diese Probleme bezogen sich auf die Migration von visuellen Angeboten zu Angebotsvorlagen.

## „at.js“-Version 0.9.6

**Datum:** 13. April 2017

Die folgenden Verbesserungen und Fehlerbehebungen sind in at.js-Version 0.9.6 enthalten:

* Unterstützung für Umleitungsangebote für A4T. Nach dem Herunterladen und Installieren der at.js-Version 0.9.6 können Sie Umleitungsangebote in Aktivitäten verwenden, die [!UICONTROL Adobe Analytics as the Reporting Source for Target] (A4T) verwenden. Neben at.js Version 0.9.6 gibt es weitere Mindestanforderungen, die Ihre Implementierung erfüllen muss, um Umleitungsangebote und A4T nutzen zu können. Weitere wichtige Informationen finden Sie unter [Umleitungsangebote – A4T-FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html).
* Vor at.js 0.9.6 galt: Wenn eine Besucher-API auf der Seite vorhanden und die `visitorApiTimeout` [!DNL Target] zu aggressiv war, konnte dies dazu führen, dass in der [!DNL Target]-Anfrage keine ECID-Daten gesendet wurden. So konnte es bei der Verwendung von A4T zu Problemen wie z. B. aufgetrennten Treffern in [!DNL Analytics] kommen.

  Dieses Verhalten wurde in at.js 0.9.6 geändert. Selbst wenn die `visitorApiTimeout` auf 1 ms eingestellt ist, versucht [!DNL Target], SDID-, Tracking-Server- und Kunden-IDs-Daten zu erfassen und in der [!DNL Target]-Anfrage zu senden.

* Die Einstellung `selectorsPollingTimeout` wurde hinzugefügt. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).
* Das Antwortformat von `getOffer()` wurde geändert. Weitere Informationen finden Sie unter [adobe.target.getOffer(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md).
* Die Konsolenprotokollierung für nicht unterstützte `<!DOCTYPE>`-Deklarationen wurde hinzugefügt.
* Es wurde ein Problem behoben, bei dem [!DNL Target Classic] Plug-ins nicht korrekt angewendet wurden, wenn mehrere Standardangebote an eine einzelne Mbox gesendet wurden. (TGT-22664)
* Die Cookie-Einstellung für zwei Domains auf oberster Ebene (TLDs) mit zwei Buchstaben wurde verbessert, um sicherzustellen, dass das mbox-Cookie für diese Domains korrekt festgelegt wird (z. B. test.no, autodrives.ca usw.).
* Der Algorithmus zum Extrahieren der Domain der obersten Ebene, die beim Speichern von Cookies verwendet werden sollte, hat sich in at.js-Version 0.9.6 geändert. Aufgrund dieser Änderung können keine Cookies für Adressen gespeichert werden, die IP verwenden. IP-Adressen werden größtenteils zu Testzwecken verwendet. Als Problemumgehung können Sie jedoch DNS-Einträge verwenden oder die Hosts-Datei auf einer lokalen Box anpassen.
* Die Verarbeitung von Aktionen zum Verschieben und Neuanordnen bei Zeichenfolgenwerten anstelle von Ganzzahlen als Eigenschaften wurde korrigiert.

## „at.js“-Version 0.9.4

**Datum:** 19. Januar 2017

* Mbox-Namen können jetzt Sonderzeichen wie das kaufmännische Und ( &amp; ) enthalten.

  Eine Liste der zulässigen Sonderzeichen finden Sie unter [at.js-Konfiguration](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

* Die Funktion `secureOnly` wurde hinzugefügt, die anzeigt, ob at.js nur HTTPS verwenden soll oder ob es möglich ist, dass basierend auf dem Seitenprotokoll zwischen HTTP und HTTPS umgeschaltet wird. Es handelt sich hierbei um eine erweiterte Einstellung, deren Standardwert „false“ (falsch) lautet und die von `targetGlobalSettings` überschrieben werden kann.
* Die Option „Legacy-Browser-Unterstützung“ ist in at.js-Version 0.9.3 und früher verfügbar. Diese Option wurde in at.js, Version 0.9.4 entfernt.

## „at.js“-Version 0.9.3

**Datum:** 10. Oktober 2016

* Stellt sicher, dass Mbox-Aufrufe in Microsoft Internet Explorer 11 ausgelöst werden, wenn veraltete Browser in den at.js-Einstellungen deaktiviert sind.
* Stellt sicher, dass Standardinhalte wiedergegeben werden, wenn ein dynamisches Remote-Angebot fehlschlägt (wenn beispielsweise die URL nicht korrekt ist und eine 404-Fehlermeldung angezeigt wird).
* Stellt sicher, dass Elemente schnell angezeigt werden, wenn im DOM keine Selektoren für VEC-Clicktracking gefunden werden.

## „at.js“-Version 0.9.2

**Datum:** 21. September 2016

* Es wurde die Einstellung `optoutEnabled` hinzugefügt, um die Abmeldung für Gerätediagramme zu ermöglichen. Ist diese Option als `true` eingestellt und hat sich der Besucher gegen eine Verfolgung entschieden, ruft der Browser des Benutzers die Mbox nicht auf. Gerätediagramme sind derzeit als Betaversion verfügbar. Diese Einstellung ist standardmäßig auf `false` festgelegt, muss jedoch bei Verwendung von Gerätediagramm auf `true` festgelegt werden.
* Erweiterte Unterstützung für `CustomEvent` im Benachrichtigungsmechanismus. In der Vergangenheit konnte der Ereignis-Benachrichtigungsmechanismus von at.js nicht mit Standard-DOM-APIs wie `document.addEventListener()` () verwendet werden. Jetzt können Sie `document.addEventListener()` verwenden, um at.js-Ereignisse, z. B. Abfrage- und Inhaltswiedergabe-Ereignisse, zu abonnieren.
* Es wurde ein Problem im Zusammenhang mit Angeboten behoben, die im Visual Experience Composer (VEC) erstellt wurden. Vor dieser Version hat [!DNL Target] die Selektoren ausgeblendet und die Ausblendung nur aufgehoben, wenn alle Selektoren übereinstimmen. In at.js 0.9.2 blendet [!DNL Target] die Selektoren aus, sobald sie abgeglichen werden.

## „at.js“-Version 0.9.1

**Datum:** 14. Juli 2016

* Stellt at.js eine Zeitüberschreitung für den Besucher-ID-Dienst bereit, die unabhängig von der eigenen Zeitüberschreitung des Dienstes ist.
* Korrigiert ein Problem in 0.9.0, das sich auf Implementierungen mit at.js auf einigen Seiten und mbox.js (inzwischen nicht mehr unterstützt) auf anderen Seiten auswirkte.
* Wenn Sie [!DNL Adobe Analytics] als Berichtsquelle für Ihre Aktivität verwenden, müssen Sie bei der Erstellung der Aktivität keinen Trackingserver angeben, wenn Sie mbox.js Version 61 (oder höher) oder at.js Version 0.9.1 (oder höher) verwenden. Die at.js-Bibliothek sendet automatisch Tracking-Server-Werte an [!DNL Target]. Bei der Erstellung einer Aktivität können Sie das Feld Tracking Server auf der Seite Ziele und Einstellungen leer lassen.

## „at.js“-Version 0.9.0

**[!DNL Target]Version:** 16.6.1

**Datum:** 23. Juni 2016

* Behebung eines Whitescreen-Problems bei der Verwendung von VEC-Angeboten. Jeder, der at.js verwendet, sollte ein Upgrade auf diese neue Version durchführen.
* Neue `registerExtension`-API.

  Diese neue API bietet Entwicklern Zugriff auf bestimmte jQuery-Module, die in at.js zur Entwicklung von Erweiterungen (auch als Plug-ins bezeichnet) für die -Bibliothek verwendet werden. Für diese Änderung gibt es verschiedene Gründe. Die Änderung wirkt sich nur auf Benutzer aus, die mit folgenden Funktionen arbeiten:

   * Die `getSettings()`-API wurde entfernt, die gleichen Funktionen sind aber über `registerExtension()` verfügbar.
   * Die `getTracking()`-API wurde entfernt, die gleichen Funktionen sind aber über `registerExtension()` verfügbar.

   * Bestehende Erweiterungen (z. B. Erweiterungen für AngularJS) müssen aktualisiert werden, damit `registerExtension()` verwendet werden kann.

* Neue at.js-Benachrichtigungs-API.

  Dieses Benachrichtigungssystem soll Ihnen einen besseren Einblick geben, was at.js auf der Seite tut und wann es Probleme gibt. Ein häufig im VEC auftretendes Problem ist, dass sich bei einem IT-Release die Seite ändert. Somit wird ein VEC-Selektor beschädigt und der Test kann Inhalte nicht mehr ordnungsgemäß bereitstellen. Ziel dieses Benachrichtigungssystems ist es, die Seite auf dieses Bereitstellungsproblem aufmerksam zu machen, sodass Entwickler auf die Informationen zugreifen, sie an ein System wie [!DNL Adobe Analytics] weiterleiten und Nachrichten an den Geschäftsinhaber übermitteln können, um darüber zu informieren, dass der Test nicht mehr funktioniert.

* Neue `targetGlobalSettings()`-API-Methode.

  Sie können Einstellungen in der at.js-Bibliothek überschreiben, anstatt sie in der [!DNL Target Standard/Premium]-Benutzeroberfläche oder durch Verwendung von REST-APIs zu konfigurieren.

## „at.js“-Version 0.8.0

**Datum:** 5. Mai 2016.

Dies ist die erste offizielle Version der „at.js“-Bibliothek.

at.js ist eine neue Implementierungsbibliothek für [!DNL Target], die sowohl für typische Web-Implementierungen als auch für Single Page Applications (SPA) ausgelegt ist.

at.js ersetzt mbox.js für [!DNL Adobe Target]-Implementierungen.

Neben anderen Vorteilen verbessert at.js die Seitenladezeiten für Web-Implementierungen, verbessert die Sicherheit und bietet bessere Implementierungsoptionen für Single-Page-Anwendungen.

„at.js “ enthält die Komponenten, die sich in „target.js“ befanden, weshalb kein Aufruf mehr an „target.js“ erfolgt.

Achten Sie bei der Implementierung von „at.js“ auf Folgendes:

* Versionen von Internet Explorer, die älter als Version 8 sind, werden nicht unterstützt.
* Asynchrone Implementierung bedeutet, dass ältere Integrationen wie das [!UICONTROL Test&Target to SiteCatalyst]-Plug-in möglicherweise nicht funktionieren.
* [!DNL Target]-Plug-ins, die auf mbox.js-Objekte und -Methoden verweisen, werden nicht unterstützt.
* Alle [!DNL Target]-Aufrufe werden über XMLHTTPRequest getätigt und Inhalt wird über JSON zurückgegeben.
