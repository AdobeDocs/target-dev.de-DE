---
keywords: adobe.target.trackEvent, trackEvent, trackEvent, trackEvent, trackEvent, at.js, funktionen, function, preventionDefault, preventionDefault, preventionDefault, adobe.target.trackEvent
description: Verwenden Sie die Funktion [!UICONTROL adobe.target.trackEvent()] für die JavaScript-Bibliothek " [!DNL Adobe Target] .js“, um eine Anforderung auszulösen, Benutzeraktionen wie Klicks und Konversionen auf Ihrer Site zu melden.
title: Wie verwende ich die Funktion [!UICONTROL adobe.target.trackEvent()]?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
TQID: https://experienceleague.adobe.com/Jib9C5FvmsgIF6CA-0UbdMdnMiXxQCkU2-O3Zys3vrY
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 56%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Diese Funktion löst eine Anforderung zum Melden von Benutzeraktionen aus (wie beispielsweise Klicks und Konversionen). Sie übermittelt keine Aktivitäten in der Antwort.

Diese Mbox-Aufrufe für die Ereignisverfolgung können dann verwendet werden, um in den Aktivitäten Metriken zu definieren. Weitere Informationen finden Sie unter [Erfolgsmetriken](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) und [Konversions-Tracking](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Hier finden Sie die Einzelheiten zur API:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| mbox | Zeichenfolge | Ja | Name der Mbox<P>**Hinweis**: Wenn ein Aufruf [!UICONTROL trackEvent()] mit einem Mbox-Namen ausgelöst wird, der bereits auf der Seite ausgelöst wurde, wird die SDID von [!UICONTROL trackEvent()] zurückgesetzt und unterscheidet sich von den [!DNL Target] Aufrufen auf der Seite. Wenn Sie jedoch einen [!UICONTROL trackEvent()]-Aufruf mit einem anderen Mbox-Namen auslösen, bleibt die SDID [!UICONTROL trackEvent()]-Aufrufs konsistent mit den [!UICONTROL Seitenladeanforderung]/[!UICONTROL triggerView()]-Aufrufen auf der Seite. |
| selector | Zeichenfolge | Nein | CSS-Selektoren für die Ermittlung der HTML-Elemente Die Ereignis-Listener werden mit gefundenen Elementen verbunden. |
| Typ | Zeichenfolge | Nein | Stellt einen registrierten Ereignistyp dar. Dabei kann es sich um HTML-bekannte Ereignisse wie „click“, „mousedown“ und so weiter sowie benutzerdefinierte HTML-Ereignisse handeln. |
| preventDefault | Boolesch | Nein | Gibt an, ob `[!UICONTROL event.preventDefault()]` im Rückruf des Ereignislisteners verwendet werden soll. Standard ist „false“.<P>**Hinweis**: Nur `[!UICONTROL form[submit]]` und `a[click]` werden unterstützt. Andere Szenarien werden aufgrund der Komplexität und der sehr großen Anzahl an zu unterstützenden Szenarien nicht unterstützt. |
| params | Objekt | Nein | Mbox-Parameter Ein Objekt aus Schlüssel-Wert-Paaren mit der folgenden Struktur:<P>`{ "param1": "value1", "param2": "value2"}` |
| Zeitüberschreitung | Nummer | Nein | Zeitüberschreitung in Millisekunden<P>Wenn nichts angegeben, wird der Standardwert verwendet:<P>`...timeoutInSeconds: 0.15...}` |
| success | Funktion | Nein | Eine Rückruffunktion, mit der signalisiert wird, dass das Ereignis gemeldet wurde |
| error | Funktion | Nein | Eine Rückruffunktion, mit der signalisiert wird, dass das Ereignis nicht gemeldet werden konnte |

## Beispiel

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

plus JavaScript-Code zur Zuweisung von `trackEvent`:

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

Oder:

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>Wenn die Pflichtfelder nicht festgelegt sind, wird keine -Anfrage ausgeführt und ein Fehler ausgelöst.

