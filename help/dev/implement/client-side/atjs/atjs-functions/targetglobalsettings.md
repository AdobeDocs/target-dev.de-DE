---
keywords: serverstate, targetGlobalSettings, targetGlobalSettings, globalSettings, global settings, global settings, at.js, Funktionen, function, clientCode, clientcode, serverDomain, serverdomain, cookieDomain, serverstate5, serverstate6, serverstate7, serverstate8, serverstate9, targetGlobalSettings0, targetGlobalSettings1, targetGlobalSettings2, targetGlobalSettings Settings3, targetGlobalSettings4, targetGlobalSettings5, cookiedomain, crossDomain, crossdomain, timeout, globalMboxAutoCreate, visitorApiTimeout, defaultContentHiddenStyle, defaultContentVisibleStyle, bodyHiddenStyle, bodyHidingEnabled, imsOrgId, secureOnly, override MboxEdgeServer, overrideMboxEdgeServerTimeout, cookiedomain5, cookiedomain6, cookiedomain7, cookiedomain8, cookiedomain9, crossDomain0, crossDomain1, crossDomain2, crossDomain3, crossDomain4, crossDomain5, optoutEnabled, optout, opt selectorsPollingTimeout, dataProviders, Hybrid Personalization, deviceIdLifetime
description: Verwenden Sie die Funktion "[!UICONTROL targetGlobalSettings()]"für die JavaScript-Bibliothek " [!DNL Adobe Target] at.js", um Einstellungen zu überschreiben, anstatt die  [!DNL Target] UI- oder REST-APIs zu verwenden.
title: Wie verwende ich die Funktion "[!UICONTROL targetGlobalSettings()]"?
feature: at.js
exl-id: f6218313-6a70-448e-8555-b7b039e64b2c
source-git-commit: 12cf430b65695d38d1651f2a97df418d82d231f3
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 58%

---

# [!UICONTROL targetGlobalSettings()]

Sie können Einstellungen in der at.js-Bibliothek mit `[!UICONTROL targetGlobalSettings()]` überschreiben, anstatt sie in der Benutzeroberfläche von [!DNL Target] oder durch Verwendung von REST-APIs zu konfigurieren.

## Einstellungen

Folgende Einstellungen können überschrieben werden:

### aepSandboxId

* **Typ**: String
* **Standardwert**: null
* **Beschreibung**: Optionaler Parameter, der zum Senden der [!DNL Adobe Experience Platform] Sandbox-ID zum Freigeben der in der nicht standardmäßigen Sandbox erstellten [!DNL Adobe Experience Platform] Ziele mit [!DNL Target] verwendet wird. Wenn `aepSandboxId` nicht null ist, muss auch `aepSandboxName` angegeben werden.

### aepSandboxName

* **Typ**: String
* **Standardwert**: null
* **Beschreibung**: Optionaler Parameter, der verwendet wird, um [!DNL Adobe Experience Platform] Sandbox-Namen an in der nicht standardmäßigen Sandbox erstellte [!DNL Adobe Experience Platform]-Ziele mit [!DNL Target] zu senden. Wenn `aepSandboxName` nicht null ist, muss auch `aepSandboxId` angegeben werden.

### artifactLocation

* **Typ**: String
* **Standardwert**: Keine
* **Beschreibung**: Eine vollständig qualifizierte URL für das [auf dem Gerät vorhandene Entscheidungsregel-Artefakt](../../../server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)

### bodyHiddenStyle

* **Typ**: String
* **Standardwert**: body { opacity: 0 }
* **Beschreibung**: Wird nur verwendet, wenn `globalMboxAutocreate === true`, um die Wahrscheinlichkeit eines Flackerns zu minimieren.

  Weitere Informationen finden Sie unter [Verwaltung von Flackern mit „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

### bodyHidingEnabled

* **Typ**: Boolean
* **Standardwert**: wahr
* **Beschreibung**: Wird zur Verminderung eines Flackerns eingesetzt, wenn `target-global-mbox` verwendet wird, um in Visual Experience Composer erstellte Angebote, auch „visuelle Angebote“ genannt, bereitzustellen.

### clientCode

* **Typ**: String
* **Standardwert**: Wert, der über die Benutzeroberfläche festgelegt wird.
* **Beschreibung**: Stellt den Clientcode dar.

### cookieDomain

* **Typ**: String
* **Standardwert**: Legen Sie nach Möglichkeit die Domäne auf oberster Ebene fest.
* **Beschreibung**: Steht für die Domäne, die beim Speichern von Cookies verwendet wird.

### crossDomain

* **Typ**: String
* **Standardwert**: Wert, der über die Benutzeroberfläche festgelegt wird.
* **Beschreibung**: Gibt an, ob domänenübergreifende Verfolgung aktiviert ist oder nicht. Die zulässigen Werte hängen von Ihrer at.js-Version ab. Für at.js v1.*x* geben Sie an, ob domänenübergreifende Funktionen `disabled` sind (Browser setzen Cookies nur in Ihrer Domäne (Erstanbieter-Cookies), `x only` (Browser setzen Cookies nur in der Domäne von [!DNL Target]) oder beide durch Auswahl von `enabled` (Browser legen sowohl Erst- als auch Drittanbieter-Cookies fest). Geben Sie für at.js v2.10 und höher an, ob domänenübergreifende Funktionen `enabled` (Browser setzen sowohl Erst- als auch Drittanbieter-Cookies ein) oder `disabled` (Browser setzen keine Drittanbieter-Cookies ein) sind.

### cspScriptNonce

* **Typ**: Siehe [Content Security-Richtlinie](#content-security-policy) weiter unten.
* **Standardwert**: Siehe [Content Security-Richtlinie](#content-security-policy) weiter unten.
* **Beschreibung**: Siehe [Content Security-Richtlinie](#content-security-policy) weiter unten.

### cspStyleNonce

* **Typ**: Siehe [Content Security-Richtlinie](#content-security-policy) weiter unten.
* **Standardwert**: Siehe [Content Security-Richtlinie](#content-security-policy) weiter unten.
* **Beschreibung**: Siehe [Content Security](#content-security-policy)-Richtlinie weiter unten.

### dataProviders

* **Typ**: Siehe [Daten-Anbieter](#data-providers) weiter unten.
* **Standardwert**: Siehe [Datenanbieter](#data-providers) unten.
* **Beschreibung**: Siehe [Daten-Anbieter](#data-providers) weiter unten.

### decisioningMethod

* **Typ**: String
* **Standardwert**: Server-seitig
* **Andere Werte**: On-Device, Hybrid
* **Beschreibung**: Siehe Entscheidungsmethoden weiter unten.

  **Entscheidungsmethoden**

  Mit der Entscheidungsfindung auf dem Gerät führt [!DNL Target] eine neue Einstellung namens &quot;Decisioning Method&quot;ein, die bestimmt, wie at.js Ihre Erlebnisse bereitstellt. `decisioningMethod` hat drei Werte: nur Server-seitig, nur auf dem Gerät und hybrid. Wenn `decisioningMethod` in `targetGlobalSettings()` festgelegt ist, fungiert es als Standard-Entscheidungsmethode für alle [!DNL Target]-Entscheidungen.

  **Nur Server-seitig**:

  Nur serverseitig ist die standardmäßige Entscheidungsmethode, die vorkonfiguriert ist, wenn at.js 2.5+ implementiert und in Ihren Webeigenschaften bereitgestellt wird.

  Die Verwendung von nur serverseitig als Standardkonfiguration bedeutet, dass alle Entscheidungen im Edge-Netzwerk [!DNL Target] getroffen werden, was einen blockierenden Server-Aufruf beinhaltet. Dieser Ansatz kann zu einer inkrementellen Latenz führen, bietet aber auch erhebliche Vorteile, z. B. die Möglichkeit, die maschinellen Lernfunktionen von [!DNL Target] anzuwenden, zu denen die Aktivitäten [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) und [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) gehören.

  Darüber hinaus kann die Verbesserung Ihrer personalisierten Erlebnisse mithilfe des Benutzerprofils von [!DNL Target], das sitzungs- und kanalübergreifend beibehalten wird, leistungsstarke Ergebnisse für Ihr Unternehmen liefern.

  Schließlich können Sie nur serverseitig die Adobe Experience Cloud verwenden und Zielgruppen anpassen, die über Audience Manager- und Adobe Analytics-Segmente angesprochen werden können.

  **Nur auf dem Gerät**:

  Nur auf dem Gerät ist die Entscheidungsmethode, die in at.js 2.5 oder höher festgelegt werden muss, wenn die Entscheidungsfindung auf dem Gerät nur auf allen Webseiten verwendet werden soll.

  Die Entscheidungsfindung auf dem Gerät kann Ihre Erlebnisse und Personalisierungsaktivitäten schnell bereitstellen, da die Entscheidungen aus einem zwischengespeicherten Regelartefakt getroffen werden, das all Ihre Aktivitäten enthält, die für die Entscheidungsfindung auf dem Gerät qualifiziert sind.

  Weitere Informationen dazu, welche Aktivitäten für die Entscheidungsfindung auf dem Gerät qualifiziert sind, finden Sie im Abschnitt „Unterstützte Funktionen“.

  Diese Entscheidungsmethode sollte nur verwendet werden, wenn die Leistung auf allen Seiten, für die Entscheidungen von [!DNL Target] erforderlich sind, äußerst kritisch ist. Beachten Sie außerdem, dass bei Auswahl dieser Entscheidungsmethode Ihre [!DNL Target]-Aktivitäten, die nicht für die Entscheidungsfindung auf dem Gerät qualifiziert sind, nicht bereitgestellt bzw. ausgeführt werden. Die Bibliothek at.js 2.5+ ist so konfiguriert, dass nur nach dem zwischengespeicherten Regelartefakt gesucht wird, um Entscheidungen zu treffen.

  **Hybrid**:

  Hybrid ist die Entscheidungsmethode, die in at.js 2.5 oder höher festgelegt werden muss, wenn sowohl Entscheidungen auf dem Gerät als auch Aktivitäten, die einen Netzwerkaufruf an das Edge-Netzwerk erfordern, ausgeführt werden müssen.[!DNL Adobe Target]

  Wenn Sie sowohl Entscheidungsaktivitäten auf dem Gerät als auch Server-seitige Aktivitäten verwalten, kann es bei der Bereitstellung von [!DNL Target] auf Ihren Seiten etwas kompliziert und mühsam werden. Mit Hybrid als Entscheidungsmethode weiß [!DNL Target], wann ein Server-Aufruf an das Edge-Netzwerk für Aktivitäten erforderlich ist, die eine serverseitige Ausführung erfordern, und wann nur Entscheidungen auf dem Gerät ausgeführt werden sollen.[!DNL Adobe Target]

  Das JSON-Regelartefakt enthält Metadaten, die at.js darüber informieren, ob eine Mbox eine Server-seitige Aktivität ausführt oder eine Entscheidungsaktivität auf dem Gerät aufweist. Diese Entscheidungsmethode stellt sicher, dass Aktivitäten, die Sie schnell bereitstellen möchten, über die geräteübergreifende Entscheidungsfindung durchgeführt werden. Bei Aktivitäten, die eine leistungsfähigere ML-gesteuerte Personalisierung erfordern, erfolgt diese Aktivität über das Edge-Netzwerk [!DNL Adobe Target].

### defaultContentHiddenStyle

* **Typ**: String
* **Standardwert**: Sichtbarkeit: ausgeblendet
* **Beschreibung**: Wird nur für das Umbrechen von Mboxes verwendet, bei denen DIV mit dem Klassennamen „mboxDefault“ eingesetzt wird und die über `mboxCreate()`, `mboxUpdate()` oder `mboxDefine()` ausgeführt werden, um Standardinhalte auszublenden.

### defaultContentVisibleStyle

* **Typ**: String
* **Standardwert**: Sichtbarkeit: sichtbar 
* **Beschreibung**: Wird nur für das Umbrechen von Mboxes verwendet, bei denen DIV mit dem Klassennamen „mboxDefault“ eingesetzt wird und die über `mboxCreate()`, `mboxUpdate()` oder `mboxDefine()` ausgeführt werden, um Standardinhalte oder angewendete Angebote einzublenden.

### deviceIdLifetime

* **Typ**: Zahl
* **Standardwert**: 63244800000 ms = 2 Jahre
* **Beschreibung**: Die Dauer von `deviceId` wird in Cookies beibehalten.

>[!NOTE]
>
>Die Einstellung deviceIdLifetime kann in at.js Version 2.3.1 oder höher überschrieben werden.

### aktiviert

* **Typ**: Boolean
* **Standardwert**: wahr
* **Beschreibung**: Wenn diese Option aktiviert ist, wird automatisch eine [!DNL Target]-Anfrage zum Abrufen von Erlebnissen und DOM-Manipulationen zum Rendern der Erlebnisse ausgeführt. Außerdem können [!DNL Target]-Aufrufe manuell über `getOffer(s)` / `applyOffer(s)` ausgeführt werden.

  Wenn diese Option deaktiviert ist, werden [!DNL Target]-Anforderungen nicht automatisch oder manuell ausgeführt.

### globalMboxAutoCreate

* **Typ**: Zahl
* **Standardwert**: Wert, der über die Benutzeroberfläche festgelegt wird.
* **Beschreibung**: Gibt an, ob die globale mbox-Anfrage gestellt werden soll oder nicht.

### imsOrgId

* **Typ**: String
* **Standardwert**: wahr
* **Beschreibung**: Steht für die IMS-ORG-ID.

### optinEnabled

* **Typ**: Boolean
* **Standardwert**: falsch
* **Beschreibung**: [!DNL Target] bietet Opt-in-Funktionalität über Adobe Experience Platform, um Ihre Strategie zur Zustimmungsverwaltung zu unterstützen. Mit der Opt-in-Funktion können Kunden steuern, wie und wann das [!DNL Target]-Tag ausgelöst wird. Es gibt auch eine Option über Adobe Experience Platform, das Tag [!DNL Target] vorab zu genehmigen. Um die Möglichkeit der Verwendung von Opt-in in der [!DNL Target]-at.js-Bibliothek zu aktivieren, fügen Sie die Einstellung `optinEnabled=true` hinzu. In Adobe Experience Platform müssen Sie in der Dropdownliste DSGVO-Opt-in in der Installationsansicht der Erweiterung die Option &quot;Aktivieren&quot;auswählen. Weitere Informationen finden Sie in der [Adobe Experience Platform-Dokumentation](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md). Weitere Informationen zu dieser Einstellung in Bezug auf Datenschutz- und Datenschutzbestimmungen, einschließlich der Datenschutz-Grundverordnung (DSGVO) der Europäischen Union und des California Consumer Privacy Act (CCPA), finden Sie unter [Datenschutz- und Datenschutzbestimmungen](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md).

### optoutEnabled

* **Typ**: Boolean
* **Standardwert**: falsch
* **Beschreibung**: Gibt an, ob [!DNL Target] die Funktion Visitor API `isOptedOut()` aufrufen soll. Diese Funktion ist Teil der Aktivierung für Gerätediagramme.

### overrideMboxEdgeServer

* **Typ**: Boolean
* **Standardwert**: wahr (ab at.js-Version 1.6.2)
* **Beschreibung**: Zeigt an, ob die Domäne `<clientCode>.tt.omtrdc.net` oder die Domäne `mboxedge<clusterNumber>.tt.omtrdc.net` verwendet werden soll.

  Ist dieser Wert wahr, wird die Domäne `mboxedge<clusterNumber>.tt.omtrdc.net` in einem Cookie gespeichert. Funktioniert derzeit nicht mit [CNAME](/help/dev/before-implement/implement-cname-support-in-target.md) bei der Verwendung von at.js-Versionen vor at.js 1.8.2 und at.js 2.3.1. Wenn dies ein Problem für Sie ist, sollten Sie [at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md) evtl. auf eine neuere, unterstützte Version aktualisieren.

### overrideMboxEdgeServerTimeout

* **Typ**: Zahl
* **Standardwert**: 1860000 =>; 31 Minuten
* **Beschreibung**: Zeigt die Gültigkeitsdauer des Cookies an, in dem der Wert `mboxedge<clusterNumber>.tt.omtrdc.net` gespeichert wurde.

### pageLoadEnabled

* **Typ**: Boolean
* **Standardwert**: wahr
* **Beschreibung**: Wenn diese Option aktiviert ist, werden automatisch Erlebnisse abgerufen, die beim Laden der Seite zurückgegeben werden müssen.

### ollingInterval

* **Typ**: Zahl
* **Standardwert**: 300000 (fünf Minuten in Millisekunden)
* **Beschreibung**: Intervall, in dem at.js eine neue Version eines auf dem Gerät vorhandenen Entscheidungsartefakts abruft und den Cache aktualisiert. 300000 ist der für `pollingInterval` zulässige Mindestwert.

### secureOnly

* **Typ**: Boolean
* **Standardwert**: falsch
* **Beschreibung**: Zeigt an, ob at.js nur HTTPS verwenden sollte oder es ermöglicht wird, dass basierend auf dem Seitenprotokoll zwischen HTTP und HTTPS umgeschaltet wird. Wenn es auf „wahr“ gesetzt ist, setzt secureOnly auch die Attribute „Secure“ und „SameSite“ auf das mbox-Cookie.

### selectorsPollingTimeout

* **Typ**: Zahl
* **Standardwert**: 5000 ms = 5 s
* **Beschreibung**: In at.js 0.9.6 führte [!DNL Target] diese neue Einstellung ein, die über `targetGlobalSettings` außer Kraft gesetzt werden kann.

  `selectorsPollingTimeout` gibt an, wie lange der Kunde bereit ist, darauf zu warten, dass sämtliche über Selektoren identifizierten Elemente auf der Seite angezeigt werden.

  Über Visual Experience Composer (VEC) erstellte Aktivitäten haben Angebote, die Selektoren enthalten.

### serverDomain

* **Typ**: String
* **Standardwert**: Wert, der über die Benutzeroberfläche festgelegt wird.
* **Beschreibung**: Stellt den [!DNL Target] -Edge-Server dar.

### serverState

* **Typ**: Siehe [Hybride Personalisierung](#hybrid-personalization) weiter unten.
* **Standardwert**: Siehe [Hybride Personalisierung](#hybrid-personalization) weiter unten.
* **Beschreibung**: Siehe [Hybride Personalisierung](#hybrid-personalization) weiter unten.

### telemetryEnabled

* **Typ**: Boolean
* **Standardwert**: wahr
* **Beschreibung**: Wenn diese Option aktiviert ist, erfasst Adobe SDK-Funktionsnutzung und Leistungstelemetrikdaten. Personenbezogene Daten werden nicht erfasst.

### Zeitüberschreitung

* **Typ**: Zahl
* **Standardwert**: Wert, der über die Benutzeroberfläche festgelegt wird.
* **Beschreibung**: Stellt das [!DNL Target]-Edge-Anfrage-Timeout dar.

### viewsEnabled {#viewsenabled}

* **Typ**: Boolean
* **Standardwert**: wahr
* **Beschreibung**: Wenn diese Option aktiviert ist, werden Ansichten beim Laden der Seite automatisch abgerufen. Wenn `triggerView` aufgerufen wird, werden die entsprechenden Ansichten im Browser angezeigt. Wenn diese Option deaktiviert ist, werden Ansichten zum Zeitpunkt des Seitenladevorgangs nicht abgerufen und `triggerView` hat keine Auswirkung. Ansichten werden in at.js 2 unterstützt.*x*, zutrifft.

### visitorApiTimeout

* **Typ**: Zahl
* **Standardwert**: 2000 ms = 2 s
* **Beschreibung**: Stellt die Zeitüberschreitung der Besucher-API-Anfrage dar.

## Nutzung

Diese Funktion kann definiert werden, bevor at.js geladen wird, oder alternativ unter **Einrichten** > **Implementierung** > **at.js-Einstellungen bearbeiten** > **Code-Einstellungen** > **Bibliothekskopfzeile**.

Die Bibliothekskopfzeile ermöglicht es Ihnen, JavaScript ohne Formvorgabe zu verwenden. Der Anpassungscode sollte dem folgenden Beispiel ähneln:

```javascript {line-numbers="true"}
window.targetGlobalSettings = {
   timeout: 200, // using custom timeout
   visitorApiTimeout: 500, // using custom API timeout
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com
};
```

## Datenanbieter   {#data-providers}

Mit dieser Einstellung können Kunden Daten von Drittanbieter erfassen, z. B. Demandbase, BlueKai und benutzerdefinierte Dienste, und die Daten als Mbox-Parameter in der globalen Mbox-Anfrage an [!DNL Target] übergeben. Sie unterstützt die Sammlung von Daten von mehreren Anbietern über asynchrone und synchrone Anfragen. Mit diesem Ansatz ist es ein Leichtes, Flicker- oder Standardinhalte zu verwalten und gleichzeitig unabhängige Timeouts für die einzelnen Anbieter festzulegen, um die Auswirkungen auf die Seitenleistung zu begrenzen

>[!NOTE]
>
>Datenanbieter erfordert at.js 1.3 oder höher.

Weitere Informationen dazu finden Sie in den folgenden Videos:

| Video | Beschreibung |
|--- |--- |
| [Verwenden von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html) | Mit der Datenanbieterfunktion können Sie Dateien von Drittanbietern einfach an Target übergeben. Ein Drittanbieter kann ein Wetterdienst, ein DMP oder sogar Ihr eigener Web-Service sein. Anschließend können Sie diese Daten zur Erstellung von Zielgruppen und zielgerichtetem Inhalt und zur Aufwertung des Benutzerprofils verwenden. |
| [Implementieren von Datenanbietern in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html) | Implementierungsdetails und Beispiele zur Verwendung der dataProviders-Funktion von Adobe [!DNL Target], um Daten von Drittanbietern abzurufen und in der [!DNL Target] -Anfrage zu übergeben. |

Die Einstellung `window.targetGlobalSettings.dataProviders` entspricht einer Reihe von Datenanbietern.

Jeder Datenanbieter weist die folgende Struktur auf:

| Schlüssel | Typ | Beschreibung |
|--- |--- |--- |
| name | Zeichenfolge | Name des Anbieters. |
| version | Zeichenfolge | Anbieterversion. Dieser Schlüssel wird für die Anbieterentwicklung verwendet. |
| Zeitüberschreitung | Nummer | Gibt die Anbieter-Zeitüberschreigung an, wenn es sich hierbei um eine Netzwerkanfrage handelt.  Dieser Schlüssel ist optional. |
| provider | Funktion | Die Funktion, welche die Logik zum Abrufen der Anbieterdaten enthält.<p>Die Funktion verfügt über einen einzigen erforderlichen Parameter: `callback`. Der Parameter „callback“ ist eine Funktion, die nur aufgerufen werden sollte, wenn die Daten erfolgreich abgerufen wurden oder ein Fehler vorliegt.<p>Der Callback erwartet zwei Parameter:<ul><li>error: Gibt an, ob ein Fehler aufgetreten ist. Wenn alles in Ordnung ist, sollte dieser Parameter auf „null“ festgelegt sein.</li><li>params: Ein JSON-Objekt, das die Parameter darstellt, die in einer [!DNL Target] -Anfrage gesendet werden.</li></ul> |

Im folgenden Beispiel wird gezeigt, wo der Datenanbieter die Synchronisierungsausführung verwendet:

```javascript {line-numbers="true"}
var syncDataProvider = {
  name: "simpleDataProvider",
  version: "1.0.0",
  provider: function(callback) {
    callback(null, {t1: 1});
  }
};

window.targetGlobalSettings = {
  dataProviders: [
    syncDataProvider
  ]
};
```

Nachdem at.js `window.targetGlobalSettings.dataProviders` verarbeitet hat, enthält die [!DNL Target] -Anfrage einen neuen Parameter: `t1=1`.

Im Folgenden finden Sie ein Beispiel, wenn die Parameter, die Sie zur [!DNL Target] -Anfrage hinzufügen möchten, von einem Drittanbieter-Service wie Bluekai, Demandbase usw. abgerufen werden:

```javascript {line-numbers="true"}
var blueKaiDataProvider = {
   name: "blueKai",
   version: "1.0.0",
   provider: function(callback) {
      // simulating network request
     setTimeout(function() {
       callback(null, {t1: 1, t2: 2, t3: 3});
     }, 1000);
   }
}

window.targetGlobalSettings = {
   dataProviders: [
      blueKaiDataProvider
   ]
};
```

Nachdem at.js `window.targetGlobalSettings.dataProviders` verarbeitet hat, enthält die [!DNL Target] -Anfrage zusätzliche Parameter: `t1=1`, `t2=2` und `t3=3`.

Im folgenden Beispiel werden mithilfe von Datenanbietern Wetter-API-Daten erfasst und als Parameter in einer [!DNL Target] -Anfrage gesendet. Die [!DNL Target] -Anfrage weist zusätzliche Parameter auf, z. B. `country` und `weatherCondition`.

```javascript {line-numbers="true"}
var weatherProvider = {
      name: "weather-api",
      version: "1.0.0",
      timeout: 2000,
      provider: function(callback) {
        var API_KEY = "caa84fc6f5dc77b6372d2570458b8699";
        var lat = 44.426767399999996;
        var lon = 26.1025384;
        var url = "//api.openweathermap.org/data/2.5/weather?";
        var data = {
          lat: lat,
          lon: lon,
          appId: API_KEY
        }

        $.ajax({
          type: "GET",
                url: url,
          dataType: "json",
          data: data,
          success: function(data) {
            console.log("Weather data", data);
            callback(null, {
              country: data.sys.country,
              weatherCondition: data.weather[0].main
            });
          },
          error: function(err) {
            console.log("Error", err);
            callback(err);
          }
        });
      }
    };

    window.targetGlobalSettings = {
      dataProviders: [weatherProvider]
    };
```

Beachten Sie Folgendes, wenn Sie die Einstellung `dataProviders` verwenden.

* Wenn die `window.targetGlobalSettings.dataProviders` hinzugefügten Datenanbieter asynchron sind, werden sie parallel ausgeführt. Die Besucher-API-Anfrage wird parallel mit den `window.targetGlobalSettings.dataProviders` hinzugefügten Funktionen ausgeführt, um eine minimale Wartezeit zu ermöglichen.
* at.js versucht nicht, die Daten zwischenzuspeichern. Wenn der Datenanbieter die Daten nur einmal abruft, sollte er sicherstellen, dass die Daten zwischengespeichert werden, und die Cachedaten für den zweiten Aufruf verarbeiten, wenn die Anbieterfunktion aufgerufen wird.

## Content Security Policy

at.js 2.3.0+ unterstützt das Festlegen von Content Security Policy-Nonces für SCRIPT- und STYLE-Tags, die beim Anwenden von bereitgestellten [!DNL Target]-Angeboten an das Seiten-DOM angehängt werden.

Die SCRIPT- und STYLE-Nonces sollten vor dem Laden von at.js 2.3.0 und höher entsprechend in `targetGlobalSettings.cspScriptNonce` und `targetGlobalSettings.cspStyleNonce` festgelegt werden. Sehen Sie sich das Beispiel unten an:

```javascript {line-numbers="true"}
...
<head>
 <script nonce="<script_nonce_value>">
window.targetGlobalSettings = {
  cspScriptNonce: "<csp_script_nonce_value>",
  cspStyleNonce: "<csp_style_nonce_value>"
};
 </script>
 <script nonce="<script_nonce_value>" src="at.js"></script>
...
</head>
...
```

Nachdem die Einstellungen `cspScriptNonce` und `cspStyleNonce` festgelegt wurden, legt at.js 2.3.0+ diese als Nonce-Attribute für alle SCRIPT- und STYLE-Tags fest, die beim Anwenden von [!DNL Target] Angeboten an das DOM angehängt werden.

## Hybride Personalisierung

`serverState` ist eine Einstellung, die in at.js v2.2+ verfügbar ist und mit der die Seitenleistung optimiert werden kann, wenn eine Hybridintegration von [!DNL Target] implementiert ist. Hybride Integration bedeutet, dass Sie sowohl at.js v2.2+ auf Client-Seite als auch die Bereitstellungs-API oder ein [!DNL Target] SDK auf Server-Seite verwenden, um Erlebnisse bereitzustellen. `serverState` ermöglicht at.js v2.2+, Erlebnisse direkt aus Inhalten anzuwenden, die auf Serverseite abgerufen und als Teil der bereitzustellenden Seite an den Client zurückgegeben wurden.

### Voraussetzungen

Sie müssen über eine hybride Integration von [!DNL Target] verfügen.

* **Server-seitig**: Sie müssen die [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) oder die [Target-SDKs](/help/dev/implement/server-side/sdk-guides/getting-started/getting-started.md) verwenden.
* **Client-seitig**: Sie müssen [at.js, Version 2.2 oder neuer](/help/dev/implement/client-side/atjs/target-atjs-versions.md) verwenden.

### Code-Beispiele

Um besser zu verstehen, wie dies funktioniert, sehen Sie sich die Code-Beispiele unten an, die Sie auf Ihrem Server haben würden. Der Code setzt voraus, dass Sie das [Target Node.js-SDK](https://github.com/adobe/target-nodejs-sdk) verwenden.

```javascript {line-numbers="true"}
// First, we fetch the offers via Target Node.js SDK API, as usual
const targetResponse = await targetClient.getOffers(options);
// A successfull response will contain Target Delivery API request and response objects, which we need to set as serverState
const serverState = {
  request: targetResponse.request,
  response: targetResponse.response
};
// Finally, we should set window.targetGlobalSettings.serverState in the returned page, by replacing it in a page template, for example
const PAGE_TEMPLATE = `
<!doctype html>
<html>
<head>
  ...
  <script>
    window.targetGlobalSettings = {
      overrideMboxEdgeServer: true,
      serverState: ${JSON.stringify(serverState, null, " ")}
    };
  </script>
  <script src="at.js"></script>
</head>
...
</html>
`;
// Return PAGE_TEMPLATE to the client ...
```

Ein Beispiel für `serverState`-Objekt-JSON für den Vorab-Abruf der Ansicht sieht wie folgt aus:

```javascript {line-numbers="true"}
{
 "request": {
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "context": {
   "channel": "web",
   "timeOffsetInMinutes": 0
  },
  "experienceCloud": {
   "analytics": {
    "logging": "server_side",
    "supplementalDataId": "7D3AA246CC99FD7F-1B3DD2E75595498E"
   }
  },
  "prefetch": {
   "views": [
    {
     "address": {
      "url": "my.testsite.com/"
     }
    }
   ]
  }
 },
 "response": {
  "status": 200,
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "testclient",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
   "views": [
    {
     "name": "home",
     "key": "home",
     "options": [
      {
       "type": "actions",
       "content": [
        {
         "type": "setHtml",
         "selector": "#app > DIV.app-container:eq(0) > DIV.page-container:eq(0) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
         "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
         "content": "<span style=\"color:#FF0000;\">Latest</span> Products for 2020"
        }
       ],
       "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
       "responseTokens": {
        "profile.memberlevel": "0",
        "geo.city": "dublin",
        "activity.id": "302740",
        "experience.name": "Experience B",
        "geo.country": "ireland"
       }
      }
     ],
     "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    }
   ]
  }
 }
}
```

Nachdem die Seite im Browser geladen wurde, wendet at.js alle [!DNL Target]-Angebote von `serverState` sofort an, ohne Netzwerkaufrufe an den [!DNL Target]-Edge auszulösen. Darüber hinaus blendet at.js nur die DOM-Elemente vorab aus, für die im Server-seitig abgerufenen Inhalt [!DNL Target]-Angebote verfügbar sind, was sich positiv auf die Seitenladeleistung und das Endbenutzererlebnis auswirkt.

### Wichtige Hinweise

Beachten Sie bei der Verwendung von `serverState` Folgendes:

* Derzeit unterstützt at.js v2.2 nur die Bereitstellung von Erlebnissen über serverState für:

   * Mit VEC erstellte Aktivitäten, die beim Laden der Seite ausgeführt werden.
   * Vorab abgerufene Ansichten.

     Bei SPA Verwendung von [!DNL Target] Ansichten und `triggerView()` in der at.js-API speichert at.js v2.2 den Inhalt für alle Ansichten, die vorab auf der Server-Seite abgerufen werden, zwischen und wendet diese an, sobald jede Ansicht über `triggerView()` ausgelöst wird, erneut ohne dass zusätzliche Aufrufe zum Abrufen von Inhalten an [!DNL Target] ausgelöst werden.

   * **Hinweis**: Derzeit werden auf der Server-Seite abgerufene mboxes in `serverState` nicht unterstützt.

* Beim Anwenden von `serverState` -Angeboten berücksichtigt at.js die Einstellungen `pageLoadEnabled` und `viewsEnabled`, z. B. werden Seitenladeangebote nicht angewendet, wenn die Einstellung `pageLoadEnabled` auf &quot;false&quot;gesetzt ist.

  Um diese Einstellungen zu aktivieren, aktivieren Sie den Umschalter in **Administration > Implementierung > Bearbeiten > Seite laden aktiviert**.

  ![Einstellungen für „Seitenladen aktiviert“](../../assets/page-load-enabled-setting.png)

* Stellen Sie bei Verwendung von `serverState` und gleichzeitiger Verwendung von `<script>`-Tags im zurückgegebenen Inhalt sicher, dass Ihr HTML-Inhalt `<\/script>` statt `</script>` verwendet. Wenn Sie `</script>` verwenden, interpretiert der Browser `</script>` als Ende auf einem Inline-SCRIPT und es kann zur Beschädigung der HTML-Seite kommen.

### Zusätzliche Ressourcen

Weitere Informationen zur Funktionsweise von `serverState` finden Sie in den folgenden Ressourcen:

* [Beispielcode](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/advanced-atjs-integration-serverstate).
* [Beispielprogramm für SPAs mit `serverState`](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/react-shopping-cart-demo).
