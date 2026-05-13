---
keywords: Implementierung, JavaScript-Bibliothek, js, atjs, Entscheidungsfindung auf dem Gerät, Entscheidungsfindung auf dem Gerät, at.js, On-Device, On-Device, Fehlerbehebung, Fehlerbehebung, Implementierung2
description: Erfahren Sie, wie Sie [!UICONTROL on-device decisioning] mit der at.js-Bibliothek beheben.
title: Wie kann ich Fehler bei der geräteinternen Entscheidungsfindung mit der at.js-JavaScript-Bibliothek beheben?
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
TQID: https://experienceleague.adobe.com/Ji3jAHC0Ek7FrVnabEEMm-KCtxJLJ5rSz4uyi6sWpiE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Fehlerbehebung bei [!UICONTROL on-device decisioning] für at.js

Führen Sie die folgenden Schritte aus, um [!UICONTROL on-device decisioning] in [!UICONTROL Adobe Target] mit der at.js-JavaScript-Bibliothek zu beheben:

## Schritt 1: Konsolenprotokoll für at.js aktivieren

Durch Anhängen des URL-Parameters `mboxDebug=1` kann at.js Nachrichten in der Konsole Ihres Browsers drucken.

Alle Nachrichten enthalten das Präfix „AT:“ für einen praktischen Überblick. Um sicherzustellen, dass ein Artefakt erfolgreich geladen wurde, sollte Ihr Konsolenprotokoll Meldungen ähnlich den folgenden enthalten:

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

Die folgende Abbildung zeigt diese Meldungen im Konsolenprotokoll:

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Konsolenprotokoll mit Artefaktmeldungen](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "Konsolenprotokoll mit Artefaktmeldungen"){zoomable="yes"}

## Schritt 2: Überprüfen Sie das Herunterladen des Regelartefakts auf der Registerkarte „Netzwerk“ Ihres Browsers

Öffnen Sie im Browser die Registerkarte Netzwerk .

So öffnen Sie beispielsweise DevTools in Google Chrome:

1. Drücken Sie Strg+Umschalt+J (Windows) oder Befehl+Option+J (Mac).
1. Navigieren Sie zur Registerkarte Netzwerk .
1. Filtern Sie Ihre Aufrufe nach dem Schlüsselwort „rules.json“, um sicherzustellen, dass nur die Artefaktregeldatei angezeigt wird.

   Darüber hinaus können Sie nach &quot;/delivery|rules.json/&quot; filtern, um alle Target-Aufrufe und artefaktregeln.json anzuzeigen.

   ![Registerkarte „Netzwerk“ in Google Chrome](assets/rule-json.png)

## Schritt 3: Überprüfen des Download-Regelartefakts mithilfe von benutzerdefinierten at.js-Ereignissen

Die at.js-Bibliothek sendet zwei neue benutzerdefinierte Ereignisse, um [!UICONTROL on-device decisioning] zu unterstützen.

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

Sie können abonnieren, um diese benutzerdefinierten Ereignisse in Ihrer Anwendung zu überwachen und nach Erfolg oder Misserfolg des Herunterladens der Artefaktregeldatei eine Aktion auszuführen.

Das folgende Beispiel zeigt ein Beispiel für Code, der auf Erfolgs- und Fehlerereignisse beim Herunterladen von Artefakten wartet:

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
