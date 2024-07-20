---
keywords: at.js-Versionen, at.js-Versionen, Einzelseiten-App, SPA, domänenübergreifend, domänenübergreifend
description: Erfahren Sie, wie Sie von  [!DNL Adobe Target] at.js 1.x auf at.js 2.x aktualisieren. Untersuchen Sie Systemflussdiagramme, lernen Sie neue und veraltete Funktionen kennen und vieles mehr.
title: Wie aktualisiere ich von at.js Version 1.x auf Version 2.x?
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2939'
ht-degree: 57%

---

# Aktualisieren von at.js 1.*x* bis at.js 2.*x*  

Die neueste Version von at.js [!DNL Adobe Target] bietet umfassende Funktionen, mit denen Ihr Unternehmen mithilfe von Client-seitigen Technologien der neuesten Generation Personalisierungen ausführen kann. Diese neue Version konzentriert sich auf die Aktualisierung von at.js, um harmonische Interaktionen mit Einzelseitenanwendungen (SPAs) zu ermöglichen.

Hier einige Vorteile der Verwendung von at.js 2.*x* , die in früheren Versionen nicht verfügbar sind:

* Möglichkeit zur Zwischenspeicherung aller Angebote beim Seitenladen, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren
* Drastische Verbesserung der Erlebnisse Ihrer Endbenutzer auf Ihrer Site, da Angebote sofort über den Cache angezeigt werden, ohne dass die herkömmlichen Serveraufrufe verzögert werden.
* Einfache Einrichtung mit einzeiligem Code und einmaliger Entwicklerunterstützung, damit Ihre Marketing-Experten [!UICONTROL A/B Test] - und [!UICONTROL Experience Targeting] -Aktivitäten (XT) über VEC auf Ihrer SPA erstellen und ausführen können.

## at.js 2.*x* Systemdiagramme

Die folgenden Diagramme helfen Ihnen, den Arbeitsablauf von at.js 2 zu verstehen.*x* mit Ansichten und wie dies die SPA-Integration verbessert. Eine bessere Einführung in die in at.js 2 verwendeten Konzepte.*x*, siehe [Implementierung von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Target-Ablauf mit at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Target-Ablauf mit at.js 2.x"){zoomable="yes"}

| Aufruf | Details |
| --- | --- |
| 1 | Ein Aufruf gibt die [!UICONTROL Experience Cloud ID] zurück, falls sich der Benutzer authentifiziert hat. Bei einem weiteren Aufruf wird die Kunden-ID synchronisiert. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<P>at.js kann auch asynchron mit einem optionalen Pre-hiding-Snippet geladen werden, das auf der Seite implementiert ist. |
| 3 | Es wird eine Seitenlade-Anfrage durchgeführt, in der alle konfigurierten Parameter (MCID, SDID und Kunden-ID) enthalten sind. |
| 4 | Profilskripte werden ausgeführt und anschließend in den Profilspeicher eingespeist. Der Store ruft geeignete Zielgruppen aus der Zielgruppenbibliothek ab (z. B. über [!DNL Adobe Analytics], [!DNL Audience Manager] usw. freigegebene Zielgruppen).<P>Kundenattribute werden in einem Batch-Prozess an den Profilspeicher übermittelt. |
| 5 | Basierend auf den URL-Anfrageparametern und den Profildaten entscheidet [!DNL Target], welche Aktivitäten und Erlebnisse für die aktuelle Seite und zukünftige Ansichten an den Besucher zurückgegeben werden sollen. |
| 6 | Zielgerichteter Inhalt wird zurück an die Seite übermittelt. Dieser enthält optional Profilwerte für eine weitere Personalisierung.<P>Zielgerichteter Inhalt auf der aktuellen Seite wird so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern.<P>Zielgerichteter Inhalt für Ansichten, die als Ergebnis von Benutzeraktionen in einem SPA angezeigt werden, der im Browser zwischengespeichert wird, damit er sofort ohne zusätzlichen Server-Aufruf angewendet werden kann, wenn die Ansichten über `triggerView()` ausgelöst werden. |
| 7 | [!UICONTROL Analytics]-Daten werden an Datenerfassungsserver übermittelt. |
| 8 | Zielgruppendaten werden über die SDID mit [!UICONTROL Analytics] -Daten abgeglichen und in den Berichterstellungsspeicher [!UICONTROL Analytics] verarbeitet.<P>[!UICONTROL Analytics] -Daten können dann sowohl in [!UICONTROL Analytics] als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

Egal, wo `triggerView()` in Ihrer SPA implementiert ist, werden die Ansichten und Aktionen aus dem Cache abgerufen und dem Benutzer ohne Serveraufruf gezeigt. `triggerView()` sendet außerdem eine Benachrichtigungsanfrage an das [!DNL Target]-Backend, um Impressions-Zählungen zu erhöhen und aufzuzeichnen.

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Target-Ablauf at.js 2.*x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target-Ablauf at.js 2.*x* triggerView"){zoomable="yes"}

| Aufruf | Details |
| --- | --- |
| 1 | `triggerView()` wird in der Einzelseiten-App aufgerufen, um eine Ansicht wiederzugeben und Aktionen anzuwenden, die visuelle Elemente ändern. |
| 2 | Gezielte Inhalte für die Ansicht werden aus dem Cache gelesen. |
| 3 | Die zielgerichteten Inhalte werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern. |
| 4 | Die Benachrichtigungsanfrage wird an den [!DNL Target]-Profilspeicher gesendet, damit der Besucher in der Aktivität erfasst und die Metrik erhöht wird. |
| 5 | [!UICONTROL Analytics] an Datenerfassungsserver gesendete Daten. |
| 6 | [!DNL Target] -Daten werden über die SDID mit [!UICONTROL Analytics] -Daten abgeglichen und in den [!UICONTROL Analytics] -Berichtspeicher verarbeitet. [!UICONTROL Analytics] -Daten können dann sowohl in [!UICONTROL Analytics] als auch in [!DNL Target] über A4T-Berichte angezeigt werden. |

## Bereitstellen von at.js 2 *x*  

Bereitstellen von at.js 2 *x* über Tags in der Erweiterung [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md).

>[!NOTE]
>
>Die Bereitstellung von at.js mithilfe von Tags in [!DNL Adobe Experience Platform] ist die bevorzugte Methode.
>
>Oder
>
>Manuelles Herunterladen von at.js 2.*x* verwenden die [!DNL Target] -Benutzeroberfläche und stellen sie mithilfe der [Methode Ihrer Wahl](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) bereit.

## Nicht mehr unterstützte Funktionen von at.js

Es gibt mehrere Funktionen, die in at.js 2 nicht mehr unterstützt werden.*x*.

>[!WARNING]
>
>Wenn diese veralteten Funktionen bei at.js 2 weiterhin auf Ihrer Site verwendet werden.*x* bereitgestellt ist, werden Konsolenwarnungen angezeigt. Der empfohlene Ansatz bei der Aktualisierung besteht darin, die Implementierung von at.js 2 zu testen.*x* in einer Staging-Umgebung durchlaufen, alle in der Konsole protokollierten Warnungen durchlaufen und die veralteten Funktionen auf die neuen Funktionen übersetzen, die in at.js 2 eingeführt wurden.*x*.

Sie finden die veralteten Funktionen und das zugehörige Gegenstück unten. Eine vollständige Liste der Funktionen finden Sie unter [„at.js“-Funktionen](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).

>[!NOTE]
>
>at.js 2.*x* blendet mit `mboxDefault` markierte Elemente nicht mehr automatisch aus. Kunden müssen daher die Pre-Hide-Logik entweder manuell auf der Site selbst oder über einen Tag-Manager verwalten.

### mboxCreate(mbox,params)

**Beschreibung**:

Führt eine Anfrage aus und wendet das Angebot auf das nächste DIV mit dem `mboxDefault`-Klassennamen an.

**Beispiel**:

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**at.js 2.*x*-Äquivalent**

Eine Alternative zu `mboxCreate(mbox, params)` sind `getOffer()` und `applyOffer()`.

**Beispiel**:

```html {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  var el = document.currentScript.previousElementSibling;
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2"
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: el,
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      el.style.visibility = "visible";
    }
  });
</script> 
```

### „mboxDefine()“ und „mboxUpdate()“

**Beschreibung**:

Erstellt eine interne Zuordnung zwischen einem Element und einem Mbox-Namen, führt die Anforderung jedoch nicht aus. Wird zusammen mit `mboxUpdate()` verwendet, was die Anfrage ausführt und das Angebot auf das in `mboxDefine()` von der nodeId identifizierte Element anwendet. Die Funktion kann auch dazu genutzt werden, eine Mbox zu aktualisieren, die durch `mboxCreate` initiiert wurde.

**Beispiel**:

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**at.js 2.*x*-Äquivalent**:

Eine Alternative zu `mboxDefine()` und `mboxUpdate` sind `getOffer()` und `applyOffer()`, mit Verwendung der Selektor-Option in `applyOffer()`. Mit diesem Ansatz können Sie das Angebot einem Element mit jedem CSS-Selektor zuordnen, nicht nur mit einem mit einer ID.

**Beispiel**:

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2",
      param3: "value3",
      param4: "value4" 
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: "#someId",
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      var el = document.getElementById("someId");
      el.style.visibility = "visible";
    }
  });
</script>
```

### adobe.target.registerExtension()

**Beschreibung**:

Stellt eine Standardart zur Registrierung bestimmter Erweiterungen dar.

Dies wird nicht mehr unterstützt und sollte nicht verwendet werden.

## Zusammenfassung veralteter, neuer und unterstützter at.js-Funktionen in 2.*x*  

| Methode | Unterstützt? | Neu? | Nicht mehr verwendet?<P>(Standardinhalt wird angezeigt) |
| --- | --- | --- | --- |
| `getOffer()` | Ja |  |  |
| `getOffers()` |  | Ja |  |
| `applyOffer()` | Ja |  |  |
| `applyOffers()` |  | Ja |  |
| `triggerView()` |  | Ja |  |
| `trackEvent()` | Ja |  |  |
| `mboxCreate()` |  |  | Ja |
| `mboxDefine()`<P>`mboxUpdate()` |  |  | Ja |
| `targetGlobalSettings()` | Ja |  |  |
| `Data Providers` | Ja |  |  |
| `targetPageParams()` | Ja |  |  |
| `targetPageParamsAll()` | Ja |  |  |
| `registerExtension()` |  |  | Ja |
| `At.js Custom Events` | Ja |  |  |

## Einschränkungen und Legenden

Beachten Sie die folgenden Einschränkungen und Legenden:

### Konversions-Tracking

Kunden, die `mboxCreate()` für ihr Konversions-Tracking verwenden, müssen `trackEvent()` oder `getOffer()` benutzen.

### Bereitstellung von Angeboten

Kunden, die `mboxCreate()` nicht durch `getOffer()` oder `applyOffer()` ersetzen, riskieren möglicherweise, dass Angebote nicht bereitgestellt werden.

### Kann at.js 2.*x* auf manchen Seiten verwendet werden, während at.js 1.*x* ist auf anderen Seiten vorhanden?

Ja, das Besucherprofil wird über verschiedene Seiten mit verschiedenen Versionen und Bibliotheken hinweg erhalten. Das Cookie-Format ist identisch.

### Neue API in at.js 2.*x*  

at.js 2.*x* verwendet eine neue API, die wir die Bereitstellungs-API nennen. Um zu debuggen, ob at.js den [!DNL Target] -Edge-Server korrekt aufruft, können Sie die Registerkarte &quot;Netzwerk&quot;in den Entwicklerwerkzeugen Ihres Browsers nach &quot;Bereitstellung&quot;, &quot;`tt.omtrdc.net`&quot;oder Ihrem Clientcode filtern. Sie werden außerdem feststellen, dass [!DNL Target] eine JSON-Nutzlast anstelle von Schlüssel/Wert-Paaren sendet.

### [!DNL Target] Globale Mbox wird nicht mehr verwendet

In at.js 2.*x*, sehen Sie &quot;`target-global-mbox`&quot;nicht mehr in den Netzwerkaufrufen. Stattdessen haben wir die &quot;`target-global-mbox`&quot;-Syntax in der JSON-Payload, die an die [!DNL Target] -Server gesendet wird, in &quot;`execute > pageLoad`&quot;ersetzt:

```json {line-numbers="true"}
{
  "id": {
    // ...
  },
  "context": {
    "channel": "web",
    // ...
  },
  "execute": {
    "pageLoad": {}
  }
}
```

Im Grunde wurde das Konzept der globalen Mbox eingeführt, um [!DNL Target] mitzuteilen, ob Angebote und Inhalt beim Laden der Seite abgerufen werden sollten. Daher haben wir dies in unserer neuesten Version deutlicher gemacht.

### Ist der Name der globalen Mbox in at.js nicht mehr wichtig?

Kunden können einen globalen Mbox-Namen über **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit at.js Settings]** angeben. Diese Einstellung wird von den [!DNL Target]-Edge-Servern verwendet, um „Ausführen > Seite laden“ in den globalen Mbox-Namen zu übersetzen, der in der [!DNL Target]-Benutzeroberfläche angezeigt wird. Dadurch können Kunden mit dem globalen Mbox-Namen weiterhin Server-seitige APIs, den Form-Based Composer und Profilskripts verwenden und Zielgruppen erstellen. Wir empfehlen dringend, dass Sie auch sicherstellen, dass derselbe globale Mbox-Name auch auf der Seite **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]** konfiguriert ist, falls Sie noch Seiten haben, die at.js 1.*x*, wie in den folgenden Abbildungen dargestellt.

![Dialogfeld „at.js ändern“](../assets/modify-atjs.png)

und

![Benutzerdefinierte globale Mbox](../assets/custom-global-mbox.png)

### Muss die Einstellung &quot;Globale Mbox automatisch erstellen&quot;für at.js 2 aktiviert sein.*x*?

In den meisten Fällen ja. Diese Einstellung gibt at.js 2 an.*x* , um beim Laden der Seite eine Anfrage an die [!DNL Target] -Edge-Server zu senden. Da die globale Mbox als „Ausführen > Seite laden“ übersetzt wird, sollte diese Einstellung aktiviert sein, wenn Sie eine Anfrage beim Laden der Seite auslösen möchten.

### Funktionieren vorhandene VEC-Aktivitäten weiterhin, auch wenn der Zielname der globalen Mbox nicht in at.js 2 angegeben ist.*x*?

Ja, weil „Ausführen > Seite laden“ auf dem [!DNL Target]-Backend wie `target-global-mbox` behandelt wird.

### Wenn meine formularbasierten Aktivitäten auf `target-global-mbox` zielen, funktionieren diese Aktivitäten weiterhin?

Ja, weil „Ausführen > Seite laden“ auf den [!DNL Target]-Edge-Servern wie `target-global-mbox` behandelt wird.

### Unterstützte und nicht unterstützte at.js 2.*x* Einstellungen

| Einstellung | Unterstützt? |
| --- | --- |
| X-Domäne | Nein |
| Globale Mbox automatisch erstellen | Ja |
| Globaler Mbox-Name | Ja |

### Unterstützung von domänenübergreifendem Tracking in at.js 2.x

Durch domänenübergreifendes Tracking können Besucher auf verschiedenen Domänen verbunden werden. Da für jede Domain ein neues Cookie erstellt werden muss, ist es schwierig, Besucher zu tracken, wenn sie beim Navigation von einer Domain zu einer anderen wechseln. Um domänenübergreifendes Tracking zu ermöglichen, verwendet [!DNL Target] ein Drittanbieter-Cookie, um Besucher über verschiedene Domänen hinweg zu verfolgen. Auf diese Weise können Sie eine [!DNL Target] -Aktivität erstellen, die `siteA.com` und `siteB.com` umfasst und Besuchern beim Navigieren über individuelle Domänen dasselbe Erlebnis bleibt. Diese Funktion ist mit dem Verhalten von Drittanbieter- und Erstanbieter-Cookies von [!DNL Target] verknüpft.

>[!NOTE]
>
>Das domänenübergreifende Tracking wird ab at.js 2.10 unterstützt, in at.js 2 jedoch nicht nativ.*x* vor 2.10. Domänenübergreifendes Tracking wird in at.js 2 unterstützt.*x* über die Experience Cloud ID (ECID)-Bibliothek v 4.3.0+ unterstützt.

In [!DNL Target] wird das Drittanbieter-Cookie in `<CLIENTCODE>.tt.omtrdc.net` gespeichert. Das Erstanbieter-Cookie wird in `clientdomain.com` gespeichert. Die erste Anfrage gibt HTTP-Antwort-Header zurück, die versuchen, Drittanbieter-Cookies namens `mboxSession` und `mboxPC` festzulegen. Eine Weiterleitungsanfrage wird zusammen mit einem zusätzlichen Parameter (`mboxXDomainCheck=true`) zurückgesendet. Wenn der Browser Drittanbieter-Cookies akzeptiert, enthält die Weiterleitungsanfrage diese Cookies und das Erlebnis wird zurückgegeben. Dieser Arbeitsablauf ist möglich, da wir die HTTP GET-Methode verwenden.

In at.js 2.*x*, HTTP-GET wird nicht verwendet. Stattdessen wird die HTTP-POST über at.js 2 verwendet.*x* , um JSON-Nutzlasten an [!DNL Target] Edge-Server zu senden. Die Verwendung von HTTP-POST bedeutet, dass die Weiterleitungsanfrage zur Überprüfung, ob ein Browser Drittanbieter-Cookies unterstützt, beschädigt wird. Dies liegt daran, dass HTTP GET-Anfragen idempotent sind, während HTTP POST nicht idempotent ist und nicht willkürlich wiederholt werden darf. Daher wird domänenübergreifendes Tracking in at.js 2.*x* (vor 2.10) wird nicht standardmäßig unterstützt. Nur at.js 1.*x* verfügt über native Unterstützung für domänenübergreifendes Tracking.

Um domänenübergreifendes Tracking für at.js v2.10 oder höher zu verwenden, können Sie eine der folgenden Aktionen durchführen:

1. Installieren Sie die [ECID-Bibliothek v4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=de) in Verbindung mit at.js 2.*x* installieren. Die ECID-Bibliothek hat den Zweck, persistente IDs zu verwalten, die zur domänenübergreifenden Identifizierung eines Besuchers verwendet werden können. Nach der Installation der ECID-Bibliothek v 4.3.0 + und at.js 2.*x* können Sie Aktivitäten erstellen, die mehrere Domänen umfassen und Benutzer tracken können. Beachten Sie, dass diese Funktion erst nach Ablauf der Sitzung funktioniert.

1. Wenn Sie at.js v2.10 oder höher verwenden, müssen Sie anstelle der Installation der ECID-Bibliothek die Einstellung &quot;Domänenübergreifend&quot;in der Benutzeroberfläche von [!DNL Target] unter **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** aktivieren. (Alternativ können Sie die Option _crossDomain_ im at.js-Code auf _enabled_ setzen.)

Verwenden des domänenübergreifenden Trackings für Versionen von at.js v2.*x* vor 2.10 implementieren, können Sie Option 1 oben implementieren (Installation der ECID-Bibliothek).

### Automatische Erstellung einer globalen Mbox wird unterstützt

Diese Einstellung gibt at.js 2 an.*x* , um beim Laden der Seite eine Anfrage an die [!DNL Target] -Edge-Server zu senden. Da die globale Mbox als „Ausführen > Seite laden“ übersetzt wird und dies von den [!DNL Target]-Edge-Servern interpretiert wird, sollten Kunden dies aktivieren, wenn sie eine Anfrage beim Laden der Seite auslösen möchten.

### Globaler Mbox-Name wird unterstützt

Kunden können einen globalen Mbox-Namen über **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** angeben. Diese Einstellung wird von den [!DNL Target]-Edge-Servern verwendet, um „Ausführen > Seite laden“ in den eingegebenen globalen Mbox-Namen zu übersetzen. Dadurch können Kunden weiterhin Server-seitige APIs, den formularbasierten Composer und Profilskripts verwenden und Zielgruppen erstellen, die auf die globale Mbox zielen.

### Gelten die folgenden benutzerdefinierten at.js-Ereignisse für `triggerView()` oder gilt dies nur für `applyOffer()` oder `applyOffers()`?

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

Ja, die benutzerdefinierten at.js-Ereignisse gelten auch für `triggerView()`.

### Wenn ich &quot;`triggerView()`&quot; mit &quot;&amp;lbrace;`"page" : "true"`&amp;rbrace aufrufe, wird eine Benachrichtigung an das &quot;[!DNL Target]&quot;-Backend gesendet und die Impression erhöht. Führt dies auch dazu, dass die Profilskripts ausgeführt werden?

Wenn ein Prefetch-Aufruf an das [!DNL Target]-Backend erfolgt, werden die Profilskripts ausgeführt. Anschließend werden die betroffenen Profildaten verschlüsselt und an die Client-Seite zurückgegeben. Nachdem `triggerView()` mit `{"page": "true"}` aufgerufen wurde, wird eine Benachrichtigung zusammen mit den verschlüsselten Profildaten gesendet. Dann entschlüsselt das [!DNL Target]-Backend die Profildaten und speichert sie in den Datenbanken.

### Müssen wir vor dem Aufrufen von `triggerView()` Pre-hiding-Code hinzufügen, um Flackern zu verhindern?

Nein, Sie müssen vor dem Aufrufen von `triggerView()` keinen Pre-hiding-Code hinzufügen. at.js 2.*x* verwaltet die Pre-hiding- und Flacker-Logik, bevor die Ansicht angezeigt und angewendet wird.

### Welches at.js 1.Parameter vom Typ *x* zum Erstellen von Zielgruppen werden in at.js 2 nicht unterstützt.*x*?

Die folgenden at.js 1.x-Parameter werden derzeit für die Erstellung von Zielgruppen bei der Verwendung von at.js 2 *NOT* unterstützt.*x*:

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.* Parameter (siehe unten)

### at.js 2.*x* unterstützt nicht das Erstellen von Zielgruppen unter Verwendung von vst.* Parameter

Kunden mit at.js 1.*x* konnte vst verwenden.* Mbox-Parameter zur Erstellung von Zielgruppen. Dies war eine unbeabsichtigte Nebenwirkung von at.js 1.*x* hat Mbox-Parameter an das Backend [!DNL Target] gesendet. Nach der Migration zu at.js 2.*x* können Sie mit diesen Parametern keine Zielgruppen mehr erstellen, da at.js 2.*x* sendet Mbox-Parameter unterschiedlich.

## Kompatibilität von at.js

Die folgenden Tabellen erläutern die at.js. 2.*x* Kompatibilität mit verschiedenen Aktivitätstypen, Integrationen, Funktionen und at.js-Funktionen.

### Aktivitätstypen

| Typ | Unterstützt? |
| --- | --- |
| [!UICONTROL A/B Test] | Ja |
| [!UICONTROL Auto-Allocate] | Ja |
| [!UICONTROL Auto-Target] | Ja |
| [!UICONTROL Experience Targeting] | Ja |
| [!UICONTROL Multivariate Test] | Ja |
| [!UICONTROL Automated Personalization] | Ja |
| [!DNL Recommendations] | Ja |

>[!NOTE]
>
>[!UICONTROL Auto-Target] -Aktivitäten werden über at.js 2 unterstützt.*x* und der VEC, wenn alle Änderungen auf die `Page Load Event` angewendet werden. Wenn Änderungen zu bestimmten Ansichten hinzugefügt werden, werden nur die Aktivitäten [!UICONTROL A/B Test], [!UICONTROL Auto-Allocate] und [!UICONTROL Experience Targeting] (XT) unterstützt.

### Integrationen

| Typ | Unterstützt? |
| --- | --- |
| [!UICONTROL Analytics for Target] (A4T) | Ja |
| Zielgruppen | Ja |
| Kundenattribute | Ja |
| AEM-Experience Fragments | Ja |
| [Adobe Experience Platform-Erweiterung](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | Ja |
| Debugger | Ja |
| Auditor | Regeln wurden für at.js 2 noch nicht aktualisiert.*x*   |
| Opt-in-Unterstützung für [DSGVO](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) | Dies wird in [at.js , Version 2.1.0](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019) oder neuer unterstützt. |
| AEM Enhanced Personalization mit [!DNL Adobe Target] | Nein |

### Funktionen

| Funktion | Unterstützt? |
| --- | --- |
| X-Domäne | Nein |
| Eigenschaften/Workspaces | Ja |
| QA-Links | Ja |
| Form-Based Experience Composer | Ja |
| Visual Experience Composer (VEC) | Ja |
| Benutzerspezifischer Code | Ja |
| [Antwort-Token](#response-tokens) | Ja |
| Klick-Tracking | Ja |
| Bereitstellung mehrerer Aktivitäten | Ja |
| targetGlobalSettings | Ja (jedoch nicht X-Domäne) |
| at.js-Methoden | Alles mit Ausnahme von<P>`mboxCreate()`<P>`mboxUpdate()`<P>`mboxDefine()`<P>, wodurch der Standardinhalt angezeigt wird. |

### Abfragezeichenfolge-Parameter

| Parameter | Unterstützt? |
| --- | --- |
| `?mboxDisable` | Ja |
| `?mboxDisable` | Ja |
| `?mboxTrace` | Ja |
| `?mboxSession` | Nein |
| `?mboxOverride.browserIp` | Ja |

## Antwort-Token

at.js 2.*x* verwendet genau wie at.js 1.*x* das benutzerdefinierte Ereignis `at-request-succeeded` zu den Antworttoken. Codebeispiele, die das `at-request-succeeded` benutzerdefinierte Ereignis verwenden, finden Sie unter [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html).

## at.js 1.*x* Parameter auf at.js 2.*x* Payload-Zuordnung

In diesem Abschnitt werden die Zuordnungen zwischen at.js 1.*x* und in at.js 2.*x*.

Beachten Sie vor dem Befassen mit der Parameterzuordnung, dass sich die Endpunkte, die diese Bibliotheksversionen verwenden, geändert haben:

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x* - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

Ein weiterer wichtiger Unterschied besteht darin, dass:

* at.js 1.*x* - Client-Code ist Teil des Pfads
* at.js 2.*x* - Client-Code wird als Abfragezeichenfolgenparameter gesendet, z. B.:
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

Die folgenden Abschnitte listen jeden at.js 1.*x* -Parameter, dessen Beschreibung und die entsprechenden 2.*x* JSON-Nutzlast (falls zutreffend):

### at_property

(at.js 1.*x*-Parameter)

Wird für [Unternehmens-Benutzerberechtigungen verwendet](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de).

```json {line-numbers="true"}
{
  ....
  "property": {
    "token": "1213213123122313121"
  }
  ....
}
```

### mboxHost

(at.js 1.*x*-Parameter)

Die Domäne der Seite, auf der die [!DNL Target] -Bibliothek ausgeführt wird.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "host": "test.com"
    }
  }
}
```

### webGLRenderer

(at.js 1.*x*-Parameter)

Die WEB-GL-Renderer-Funktionen des Browsers. Dies wird von unserem Geräteerkennungsmechanismus verwendet, um festzustellen, ob das Gerät des Besuchers ein Desktop, iPhone, Android-Gerät usw. ist.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "webGLRenderer": "AMD Radeon Pro 560X OpenGL Engine"
    }
  }
}
```

### mboxURL

(at.js 1.*x*-Parameter)

Die Seiten-URL.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "url": "http://test.com"
    }
  }
}
```

### mboxReferrer

(at.js 1.*x*-Parameter)

Der Seitenverweis.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "referringUrl": "http://google.com"
    }
  }
}
```

### mbox (der Name) entspricht der globalen Mbox

(at.js 1.*x*-Parameter)

Die Bereitstellungs-API hat kein globales Mbox-Konzept mehr. In der JSON-Nutzlast müssen Sie `execute > pageLoad` verwenden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "execute": {
    "pageLoad": {
       "parameters": ....
       "profileParameters": ...
       .....
    }
  }
}
```

### mbox (der Name) entspricht *nicht* der globalen Mbox

(at.js 1.*x*-Parameter)

Um einen Mbox-Namen zu verwenden, übergeben Sie ihn an `execute > mboxes`. Eine Mbox erfordert einen Index und einen Namen.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "execute": {
    "mboxes": [{
       "index": 0,
       "name": "some-mbox",
       "parameters": ....
       "profileParameters": ...
       .....
    }]
  }
}
```

### mboxId

(at.js 1.*x*-Parameter)

Wird nicht mehr länger verwendet.

### mboxCount

(at.js 1.*x*-Parameter)

Wird nicht mehr länger verwendet.

### mboxRid

(at.js 1.*x*-Parameter)

Von Downstream-Systemen verwendete Anforderungs-ID zur Hilfe beim Debugging.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

(at.js 1.*x*-Parameter)

Wird nicht mehr länger verwendet.

### mboxSession

(at.js 1.*x*-Parameter)

Sitzungs-ID wird als Abfragezeichenfolgenparameter (`sessionId`) zum Bereitstellungs-API-Endpunkt gesendet.

### mboxPC

(at.js 1.*x*-Parameter)

Die TNT-ID wird an `id > tntId` übergeben.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

(at.js 1.*x*-Parameter)

Experience Cloud-Besucher-ID wird an `id > marketingCloudVisitorId` übergeben.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` und `vst.aaaa.authState`

(at.js 1.*x* -Parameter)

Kunden-IDs sollten an `id > customerIds` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "id": {
    "customerIds": [{
       "id": "1232131",
       "integrationCode": "aaaa",
       "authenticatedState": "....."
     }]
  }
  ....
}
```

### mbox3rdPartyId

(at.js 1.*x*-Parameter)

Kunden-Drittanbieter-ID, die zur Verknüpfung verschiedener [!DNL Target]-IDs verwendet wird.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

(at.js 1.*x*-Parameter)

SDID, auch als zusätzliche Daten-ID bekannt. Sollte an `experienceCloud > analytics > supplementalDataId` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "supplementalDataId": "1212321132123131"
    }
  }
  ....
}
```

### vst.trk

(at.js 1.*x*-Parameter)

[!UICONTROL Analytics] Tracking-Server. Sollte an `experienceCloud > analytics > trackingServer` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServer": "analytics.test.com"
    }
  }
  ....
}
```

### vst.trks

(at.js 1.*x*-Parameter)

Sicherer Analytics-Tracking-Server. Sollte an `experienceCloud > analytics > trackingServerSecure` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServerSecure": "secure-analytics.test.com"
    }
  }
  ....
}
```

### mboxMCGLH

(at.js 1.*x*-Parameter)

Audience Manager-Standorthinweis. Sollte an `experienceCloud > audienceManager > locationHint` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "locationHint": 9
    }
  }
  ....
}
```

### mboxAAMB

(at.js 1.*x*-Parameter)

Audience Manager-Blob. Sollte an `experienceCloud > audienceManager > blob` übergeben werden.

at.js 2.*x* JSON-Nutzlast:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "blob": "2142342343242342"
    }
  }
  ....
}
```

### mboxVersion

(at.js 1.*x*-Parameter)

Version wird als Abfragezeichenfolgenparameter über den Versionsparameter gesendet.

## Schulungsvideo: at.js 2.*x* Architekturdiagramm ![Badge &quot;Überblick&quot;](../../assets/overview.png)

at.js 2.*x* verbessert die Unterstützung von Adobe [!DNL Target] für SPA und kann mit anderen Experience Cloud-Lösungen integriert werden. In diesem Video wird erklärt, wie alles zusammenkommt.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Siehe [Grundlagen zu at.js 2.*x* funktioniert ](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) für weitere Informationen.
