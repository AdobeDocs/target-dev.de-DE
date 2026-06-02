---
keywords: SDK vorab ausblenden, Flackern, Anti-Flackern, Vorab-Ausblenden, Legierung, at.js, Implementierung, Einverständnis, CMP, Skriptplatzierung, Inline, Extern, SDK-Auswahl
description: Erfahren Sie, wie Sie  [!DNL Adobe Target]  SDK Prehide integrieren können, um das Flackern nicht personalisierter Inhalte (Flackern) beim Laden der Seite zu vermeiden. SDK arbeitet sowohl mit Adobe Alloy (Web SDK) als auch mit at.js.
title: Handbuch zur SDK-Integration vorab ausblenden
feature: Implementation
hide: true
source-git-commit: 2f7a53b667990474dfab7ca66a8ea93d2e946548
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Handbuch zur SDK-Integration vorab ausblenden

Eine winzige synchrone JavaScript-Bibliothek, die das visuelle Flackern verhindert, das durch [!DNL Adobe Target] Personalisierung verursacht wird, die eine Seite in der Mitte des Renderings neu schreibt. Fügen Sie oben in `<head>` ein Inline-`<script>`-Tag hinzu, und die Seite wird erst angezeigt, wenn personalisierte Inhalte bereit sind oder der Sicherheits-Timer ausgelöst wird.

## Integrationsschritte {#integration-steps}

1. Laden Sie das Paket herunter.

   Verwenden Sie die Flicker Manager-Benutzeroberfläche, um `prehide.min.js` herunterzuladen. Die Datei ist mit Ihrem Client-Code und der maximalen Wartezeit vorkonfiguriert, sodass kein `PrehideConfig` erforderlich ist.

1. Betten Sie es oben in `<head>` inline ein.

   Fügen Sie den Inhalt von `prehide.min.js` direkt in ein Inline-`<script>`-Tag als erstes untergeordnetes Element von `<head>` ein. Siehe [Inline vs. extern](#inline-vs-external) , warum Inline bevorzugt wird.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Optional) Fügen Sie einen Laufzeitkonfigurationsblock hinzu.

   Nur erforderlich, wenn Sie das Bundle selbst hosten, ohne es über die Benutzeroberfläche herunterzuladen, oder wenn Sie die SDK-Auswahl überschreiben müssen. Platzieren Sie den Konfigurationsblock vor dem Prehide-Skript:

   ```html
   <script>
     window.PrehideConfig = {
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (Optional) Einverständnis per Kabel.

   Wenn Ihre Implementierung eine Consent Management Platform (CMP) verwendet, rufen Sie `window.Prehide.setConsent(...)` auf, sobald der Einverständnisstatus bekannt ist. Siehe [Einverständnisverwaltung](#consent-management).

1. Überprüfen.

   Öffnen Sie DevTools und überprüfen Sie, ob `<style id="alloy-prehiding">` (oder `at-body-style` für at.js) beim ersten Zeichnen in `<head>` angezeigt und entfernt wird, sobald die SDK-Bearbeitung abgeschlossen ist. Führen Sie `window.Prehide.getState()` in der Konsole aus, um den Laufzeitstatus zu überprüfen.

## Platzieren des Skripts {#script-placement}

>[!IMPORTANT]
>
>Die Prehide-SDK muss vor Alloy/at.js ausgeführt werden. Wenn „Alloy“ zuerst geladen wird, rendert die Seite nicht personalisierten Inhalt und rendert ihn dann erneut. Genau das ist das Flackern, das diese SDK verhindern soll.
></br>>Fügen Sie keine `async` oder `defer` zum Prehide-Skript-Tag von SDK hinzu. Die synchrone Ausführung ist erforderlich, damit die Ausblendregel eingefügt wird, bevor der Browser mit dem Layout der Seite beginnt.

Die SDK zum Vorab-Ausblenden muss früher im Dokument angezeigt werden als die [!DNL Adobe Target] SDK, die danach bereinigt wird. Die Ladereihenfolge ist nicht verhandelbar:

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## Inline vs. extern {#inline-vs-external}

Es gibt zwei Möglichkeiten, `prehide.min.js` einzubeziehen:

| Methode | Beispiel | Hinweise |
| --- | --- | --- |
| Inline (bevorzugt) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | Kein Netzwerk-Round-Trip. Die SDK wird ausgeführt, bevor etwas Anderes gerendert wird. |
| Extern (nur wenn Inline nicht möglich ist) | `<script src="/static/prehide.min.js"></script>` | Führt eine blockierende Netzwerkanfrage vor dem ersten Rendern ein. Selbst mit HTTP/2- und Edge-Caching kostet dies normalerweise 30-80 ms. |

### Warum Inline bevorzugt wird

>[!TIP]
>
>Stellen Sie das Bundle direkt in `<script>...</script>` in Ihrer HTML-Vorlage inline. Behandeln Sie sie wie einen kritischen CSS-Block: klein, inline und immer ganz oben.

* Kein Render-blockierender Abruf. Der SDK Prehide dient dazu, Ausblendregeln (*)* ersten Rendering einzufügen. Ein externes `<script src>` fügt genau in diesem kritischen Fenster einen Netzwerk-Roundtrip hinzu.
* Kein neuer Fehlermodus. Eine externe Datei kann 404, eine Zeitüberschreitung oder durch einen Ad-Blocker blockiert werden. Eine Inline-Kopie kann nicht.
* Das Paket ist winzig (~6 KB). Das Inline-Verfahren kostet weniger als ein typisches Favicon, und kein Caching-Vorteil ist so groß, dass er den zusätzlichen Roundtrip beim ersten Rendern überwiegt.
* Cache-freundlich. Wenn in der HTML-Antwort ein Inline-Vorgang ausgeführt wird, wird die SDK neben dem Rest des Dokuments von Ihrer vorhandenen Caching-Ebene (CDN- oder Browser-HTTP-Cache) zwischengespeichert.
* Kundenspezifisches Paket. Für die heruntergeladene Datei wird der Client-Code zum Zeitpunkt des Downloads eingeblendet. Inlining stellt sicher, dass jeder Besucher das richtige benutzerdefinierte Bundle ohne zusätzliche Anfrage erhält.

## Konfiguration {#configuration}

SDK akzeptiert Konfigurationen aus zwei Quellen in der Reihenfolge der Priorität. Es liest, was zuerst verfügbar ist.

### Runtime `window.PrehideConfig` (manuelle Integration)

Deklarieren Sie für selbstgehostete oder unveränderte Bundles ein config-Objekt, bevor das Prehide-Skript ausgeführt wird:

```html
<script>
  window.PrehideConfig = {
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| Feld | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `sdk` | `"alloy"` \| `"atjs"` | Nein | Die Adobe SDK wurde auf der Seite geladen. Siehe [SDK-Auswahl](#sdk-selection). |

## SDK-Auswahl {#sdk-selection}

[!DNL Adobe Target] bietet zwei Bereitstellungs-SDKs: Alloy (die moderne Web-SDK) und at.js (die klassische Bibliothek). Jeder sucht nach einem *anderen* `<style>` Element, das nach Abschluss der Personalisierung `id` wird, und entfernt es, um die Seite anzuzeigen. Die Prehide-SDK muss den entsprechenden `id` injizieren. Andernfalls bleibt die Seite ausgeblendet, bis der Sicherheits-Timer ausgelöst wird.

| `sdk` | Stil-Tag-ID eingefügt | Entfernt von | Verwendungszeitpunkt |
| --- | --- | --- | --- |
| `"alloy"` *(Standard)* | `<style id="alloy-prehiding">` | Alloy SDK on personalize-complete | Sie laden Alloy / Adobe Web SDK auf dieser Seite. |
| `"atjs"` | `<style id="at-body-style">` | at.js unter personalize-complete | Die klassische at.js-Bibliothek wird auf dieser Seite geladen. |

>[!NOTE]
>
>Bei at.js-SDK werden nur die Versionen 2.x und höher unterstützt.

### So legen Sie es fest

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>Warnung wegen Nichtübereinstimmung. Wenn Sie beim Laden von at.js `sdk: "alloy"` festlegen (oder umgekehrt), findet der SDK das zu entfernende prehide-Element nicht. Der Guard-Timer zeigt schließlich die Seite an, aber die Besucher erhalten ein längeres ausgeblendetes Fenster. Stellen Sie `sdk` immer so ein, dass es der Bibliothek entspricht, die Sie laden.

Unbekannte oder fehlende Werte werden auf `"alloy"` zurückgesetzt, sodass vorhandene Alloy-Integrationen ohne Konfigurationsänderungen weiterhin funktionieren.

## Einverständnisverwaltung {#consent-management}

>[!NOTE]
>
>* Der Einverständniswert wird nie in `window` gespeichert. Nur die Funktion wird offen gelegt; der interne Status bleibt für die SDK privat.
>* Bei Übergängen von `"out"` zu `"in"` wird die Seite nicht erneut ausgeblendet, da das erneute Ausblenden vollständig gerenderter Inhalte visuell störend sein würde.
>* `setConsent` können in einer Seitenansicht mehrmals aufgerufen werden. Jeder Aufruf ersetzt den vorherigen Status.

Die Prehide-SDK enthält eine API zur Einverständniserkennung , die mit Ihrer CMP koordiniert wird. Die Verwendung ist optional. Wenn `setConsent` nie aufgerufen wird, verhält sich die SDK wie eine standardmäßige Nicht-Einverständnis-Integration.

### API-Oberfläche

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### Funktionsweise der einzelnen Status

| Aufruf | Auswirkung auf den Wachzeitgeber | Auswirkungen auf ausgeblendete Inhalte |
| --- | --- | --- |
| `setConsent("pending")` | Aktiver Zeitgeber wird gelöscht. Es wird keine Sicherheit eingeblendet, bis das Einverständnis erledigt ist. | Selektoren bleiben unbegrenzt ausgeblendet. |
| `setConsent("in")` | gelöscht und dann mit der konfigurierten Zeitüberschreitung neu gestartet. wartet darauf, dass die Regeln aufgelöst werden, falls sie dies noch nicht getan haben. | Der Inhalt bleibt ausgeblendet, bis der SDK personalisiert wird oder der Zeitgeber für die Überwachung ausgelöst wird. |
| `setConsent("out")` | gelöscht. Die Seite wird sofort eingeblendet. | Die Seite wird sofort angezeigt. Bei Regeln, die später aufgelöst werden *wird der* nicht erneut ausgeblendet. |
| *(nie aufgerufen)* | Standardzeitgeber wird von `init()` für die konfigurierte Dauer ausgeführt. | Der Inhalt bleibt ausgeblendet, bis der SDK personalisiert wird oder der Zeitgeber für die Überwachung ausgelöst wird. (Abwärtskompatibler Legacy-Modus.) |

### Empfohlenes Muster: explizite ausstehende Phase

1. Sobald Ihr CMP die Einverständnis-Benutzeroberfläche anzeigt, rufen Sie `setConsent("pending")` auf. Damit wird der Sicherheits-Timer gelöscht, sodass die Seite ausgeblendet bleibt, während der Besucher die Entscheidung trifft, und ein Flash von nicht personalisiertem Inhalt hinter dem Banner verhindert wird.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. Wenn der Besucher die Personalisierung akzeptiert, rufen Sie `setConsent("in")` auf. Der Guard-Timer wird neu gestartet und Alloy/at.js übernimmt die Aufgabe und zeigt die Seite an, sobald die Personalisierung angewendet wurde.

   ```js
   window.Prehide.setConsent("in");
   ```

1. Wenn der Besucher die Personalisierung ablehnt, rufen Sie `setConsent("out")` auf. Die Seite wird sofort angezeigt und bleibt sichtbar. CDN-Regeln, die später aufgelöst werden, blenden sie nicht erneut aus.

   ```js
   window.Prehide.setConsent("out");
   ```

### Beispiel: Integration im OneTrust-Stil

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### Beispiel: TCF / IAB-Style

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

