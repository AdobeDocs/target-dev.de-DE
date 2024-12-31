---
keywords: Flimmern, at.js, Implementierung, asynchron, asynchron, synchron, synchron, $8
description: Erfahren Sie, wie at.js und [!DNL Target] Flimmern verhindern (Standardinhalt wird vorübergehend angezeigt, bevor er durch Aktivitätsinhalte ersetzt wird) beim Laden von Seiten oder Apps.
title: Wie verwaltet at.js Flackern?
feature: at.js
exl-id: 8aacf254-ec3d-4831-89bb-db7f163b3869
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 57%

---

# Verwaltung von Flackern mit „at.js“

Informationen dazu, wie die [!DNL Adobe Target] at.js-JavaScript-Bibliothek Flackern beim Laden von Seiten oder Apps verhindert.

Ein Flackern tritt dann auf, wenn Besuchern vorübergehend Standardinhalt angezeigt wird, bevor dieser durch den Inhalt der entsprechenden Aktivität ersetzt werden konnte. Das Auftreten eines solchen Flackerns ist nicht wünschenswert, da es die Besucher möglicherweise verwirrt.

## Verwenden einer automatisch erstellten globalen Mbox

Wenn Sie die Einstellung [Globale Mbox automatisch erstellen](/help/dev/implement/client-side/atjs/global-mbox/customize-global-mbox.md) bei der Konfigurierung von at.js aktivieren, reduziert at.js Flackern durch Ändern der Deckkrafteinstellung beim Laden der Seite. Beim Laden von at.js wird die Deckkrafteinstellung des `<body>`-Elements in „0“ geändert, sodass die Seite für Besuchende zunächst unsichtbar wird. Nachdem eine Antwort von [!DNL Target] eingegangen ist - oder wenn ein Fehler mit der [!DNL Target]-Anfrage erkannt wird - setzt at.js die Deckkraft auf „1“ zurück. So wird gewährleistet, dass der Besucher die Seite erst sieht, nachdem der Inhalt Ihrer Aktivitäten angewendet wurde.

Wenn Sie die Einstellung bei der Konfiguration von at.js aktivieren, wird die Deckkraft des HTML-BODY von at.js auf 0 gesetzt. Nachdem eine Antwort von [!DNL Target] eingegangen ist, setzt at.js die Deckkraft des HTML-Textkörpers auf 1 zurück.

Mit einer Deckkraft von 0 ist der Seiteninhalt nicht sichtbar, sodass Flackern verhindert wird. Der Browser kann die Seite jedoch bereits rendern und lädt alle nötigen Assets wie CSS, Bilder usw.

Wenn `opacity: 0` in Ihrer Implementierung nicht funktioniert, können Sie Flackern auch handhaben, indem Sie `bodyHiddenStyle` anpassen und auf `body {visibility:hidden !important}` setzen. Sie können entweder `body {opacity:0 !important}` oder `body {visibility:hidden !important}` verwenden, je nachdem, was für Ihre spezifischen Umstände am besten geeignet ist.

Die folgende Abbildung zeigt die Aufrufe „Hide Body“ und „Show Body“ sowohl in at.js 1.*x* als auch in at.js 2.x.

**at.js 2.x**

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Target-Fluss: at.js-Seitenladeanfrage](/help/dev/implement/client-side/assets/atjs-20-flow-page-load-request.png "Target-Fluss: at.js-Seitenladeanfrage"){zoomable="yes"}

**at.js 1.*x***  

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Target-Fluss: Automatisch erstellte globale Mbox](/help/dev/implement/client-side/atjs/how-atjs-works/assets/target-flow2.png "Target-Fluss: Automatisch erstellte globale Mbox"){zoomable="yes"}

Weitere Informationen zum Überschreiben mit `bodyHiddenStyle` finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Vermeiden von Flackern beim asynchronen Laden von at.js

Das asynchrone Laden von at.js eignet sich hervorragend, um zu verhindern, dass das Rendern des Browsers blockiert wird. Bei dieser Technik kann es jedoch zu Flackereffekten auf der Webseite kommen.

Um ein Flackern zu vermeiden, können Sie ein pre-hiding-Snippet verwenden, das angezeigt wird, nachdem die entsprechenden HTML-Elemente von Target personalisiert wurden.

at.js kann asynchron geladen werden, entweder direkt in die Seite eingebettet oder über einen Tag-Manager (z. B. Adobe Experience Platform Launch).

Wenn at.js auf der Seite eingebettet ist, muss das Snippet vor dem Laden von at.js hinzugefügt werden. Wenn Sie at.js über einen Tag-Manager laden, der ebenfalls asynchron geladen wird, müssen Sie das Snippet hinzufügen, bevor Sie den Tag-Manager laden. Wenn der Tag-Manager synchron geladen wird, kann das Skript vor „at.js“ im Tag-Manager enthalten sein.

Der Code für den vorab ausgeblendeten Ausschnitt lautet wie folgt:

```
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Standardmäßig wird durch den Ausschnitt der gesamte HTML-BODY vorab ausgeblendet. Ein einigen Fällen sollten nur bestimmte HTML-Elemente vorab ausgeblendet werden und nicht die gesamte Seite. Dazu können Sie den Stilparameter anpassen. Er kann durch einen Parameter ersetzt werden, der nur bestimmte Teile der Seite vorab ausblendet.

Beispiel: Sie haben zwei Bereiche, die durch die IDs container-1 und container-2 identifiziert werden. In diesem Fall kann der Stil wie folgt ersetzt werden:

```
#container-1, #container-2 {opacity: 0 !important}
```

Anstelle der Standardeinstellung:

```
body {opacity: 0 !important}
```

## Verwalten von Flackern in at.js 2.x für triggerView()

Wenn Sie `triggerView()` benutzen, um zielgerichtete Inhalte in Ihrer SPA anzuzeigen, wird das Flackern vorkonfiguriert gehandhabt. Das bedeutet, dass die Pre-hiding-Logik nicht manuell hinzugefügt werden muss. Stattdessen blendet at.js 2.x im Voraus den Ort aus, an dem Ihre Ansicht angezeigt werden muss, bevor der zielgerichtete Inhalt angewendet wird.

## Verwalten von Flackern mit getOffer() und applyOffer()

Da es sich sowohl bei `getOffer()` als auch bei `applyOffer()` um einfache APIs handelt, sind keine Mechanismen zur Flackerverhinderung integriert. Sie können einen Selektor oder ein HTML-Element als Option an `applyOffer()` übermitteln. In diesem Fall fügt `applyOffer()` den Aktivitätsinhalt diesem Element zu, wobei Sie jedoch gewährleisten müssen, dass das Element vor dem Aufruf von `getOffer()` und `applyOffer()` vollständig ausgeblendet wurde.

```
document.documentElement.style.opacity = "0";
 
adobe.target.getOffer({
    mbox: 'target-global-mbox',
    success: function(offer) {
        adobe.target.applyOffer({
            mbox: 'target-global-mbox',
            offer: offer
        });
 
        document.documentElement.style.opacity = "1";
    },
    error: function() {
        document.documentElement.style.opacity = "1";        
    }
});
```

## Verwenden einer regionalen Mbox mit mboxCreate() in at.js 1.x (in at.js 2.x nicht unterstützt)

Wenn Sie eine regionale Mbox-Implementierung verwenden, können Sie mit `mboxCreate()` mit Ihrer Seite ähnlich dem folgenden Beispielcode arbeiten:

```
<div class="mboxDefault">
Some default content
</div>
<script>
mboxCreate('some-mbox');
</script>
```

Wurden die Seiten ordnungsgemäß bereitgestellt, verhindert at.js ein Flackern, indem die Eigenschaft CSS-„Sichtbarkeit“ des Elements mit mboxDefault-Klasse automatisch umgestellt wird.
