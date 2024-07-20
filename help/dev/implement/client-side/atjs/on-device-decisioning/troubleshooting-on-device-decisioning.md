---
keywords: Implementierung, JavaScript-Bibliothek, JS, at.js, Entscheidungsfindung auf dem Gerät, Geräteentscheidung, at.js, auf dem Gerät, auf dem Gerät, Fehlerbehebung, Problembehebung, Implementierung2
description: Erfahren Sie, wie Sie mit der at.js-Bibliothek eine Fehlerbehebung für [!UICONTROL on-device decisioning] durchführen.
title: Wie kann ich eine Fehlerbehebung bei der On-Device-Entscheidungsfindung mit der JavaScript-Bibliothek at.js durchführen?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Fehlerbehebung [!UICONTROL on-device decisioning] für at.js

Führen Sie die folgenden Schritte aus, um eine Fehlerbehebung bei [!UICONTROL on-device decisioning] in [!UICONTROL Adobe Target] mit der JavaScript-Bibliothek at.js durchzuführen:

## Schritt 1: Aktivieren des Konsolenprotokolls für at.js

Wenn Sie den URL-Parameter `mboxDebug=1` anhängen, kann at.js Nachrichten in der Browser-Konsole drucken.

Alle Nachrichten enthalten das Präfix &quot;AT:&quot;, um einen einfachen Überblick zu erhalten. Um sicherzustellen, dass ein Artefakt erfolgreich geladen wurde, sollte Ihr Konsolenprotokoll Meldungen ähnlich den folgenden enthalten:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

Die folgende Abbildung zeigt diese Meldungen im Konsolenprotokoll:

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Konsolenprotokoll mit Artefaktmeldungen](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Konsolenprotokoll mit Artefaktmeldungen"){zoomable="yes"}

## Schritt 2: Überprüfen des Herunterladens des Regelartefakts auf der Registerkarte &quot;Netzwerk&quot;Ihres Browsers

Öffnen Sie die Registerkarte Netzwerk Ihres Browsers.

So öffnen Sie beispielsweise DevTools in Google Chrome:

1. Drücken Sie Strg+Umschalt+J (Windows) bzw. Befehlstaste+Wahltaste+J (Mac).
1. Navigieren Sie zur Registerkarte Netzwerk .
1. Filtern Sie Ihre Aufrufe nach dem Keyword &quot;rules.json&quot;, um sicherzustellen, dass nur die Datei mit den Artefaktregeln angezeigt wird.

   Darüber hinaus können Sie nach &quot;/delivery|rules.json/&quot;filtern, um alle Target-Aufrufe und die Datei &quot;artifact rules.json&quot;anzuzeigen.

   Registerkarte &quot;Netzwerk&quot;in Google Chrome](assets/rule-json.png)![

## Schritt 3: Überprüfen des Herunterladens des Regelartefakts mithilfe benutzerdefinierter at.js-Ereignisse

Die at.js-Bibliothek sendet zwei neue benutzerspezifische Ereignisse, um [!UICONTROL on-device decisioning] zu unterstützen.

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Sie können diese benutzerdefinierten Ereignisse in Ihrer Anwendung abonnieren, um sie bei Erfolg oder Fehlschlagen des Dateidownloads für Artefaktregeln zu überwachen.

Das folgende Beispiel zeigt ein Beispiel für Code, der auf Erfolgs- und Fehlerereignisse beim Artefakt-Download wartet:

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
