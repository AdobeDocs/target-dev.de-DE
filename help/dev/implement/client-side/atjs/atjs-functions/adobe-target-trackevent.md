---
keywords: adobe.target.trackEvent, trackEvent, trackevent, track event, at.js, Funktionen, function, preventDefault, vermeiddefault, Standard verhindern, adobe.target.trackEvent
description: Verwenden Sie die [!UICONTROL adobe.target.trackEvent()] -Funktion für [!DNL Adobe Target] at.js-JavaScript-Bibliothek , um eine Anforderung zum Reporting von Benutzeraktionen auszulösen, z. B. Klicks und Konversionen auf Ihrer Site.
title: Wie verwende ich die [!UICONTROL adobe.target.trackEvent()] Funktion?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 59%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Diese Funktion löst eine Anforderung zum Melden von Benutzeraktionen aus (wie beispielsweise Klicks und Konversionen). Sie übermittelt keine Aktivitäten in der Antwort.

Diese Mbox-Aufrufe für die Ereignisverfolgung können dann verwendet werden, um in den Aktivitäten Metriken zu definieren. Weitere Informationen finden Sie unter [Erfolgsmetriken](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) und [Konversions-Tracking](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Hier finden Sie die Einzelheiten zur API:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| mbox | Zeichenfolge | Ja | Name der Mbox<P>**Hinweis**: Wenn eine [!UICONTROL trackEvent()] wird mit einem Mbox-Namen ausgelöst, der bereits auf der Seite ausgelöst wurde, der SDID von [!UICONTROL trackEvent()] zurückgesetzt wird und sich von der [!DNL Target] -Aufrufe auf der Seite. Das Auslösen einer [!UICONTROL trackEvent()] -Aufruf mit einem anderen Mbox-Namen behält die [!UICONTROL trackEvent()] Die SDID des Aufrufs entspricht der [!UICONTROL Seitenladeanforderung]/[!UICONTROL triggerView()] -Aufrufe auf der Seite. |
| selector | Zeichenfolge | Nein | CSS-Selektoren für die Ermittlung der HTML-Elemente Die Ereignislistener werden an die gefundenen Elemente angefügt.. |
| Typ | Zeichenfolge | Nein | Stellt einen registrierten Ereignistyp dar. Dabei kann es sich um HTML-bekannte Ereignisse wie „click“, „mousedown“ und so weiter sowie benutzerdefinierte HTML-Ereignisse handeln. |
| preventDefault | Boolesch | Nein | Gibt an, ob `[!UICONTROL event.preventDefault()]` im Rückruf des Ereignislisteners verwendet werden soll. Standard ist „false“.<P>**Hinweis**: Nur `[!UICONTROL form[submit]]` und `a[click]` werden unterstützt. Andere Szenarien werden aufgrund der Komplexität und der sehr großen Anzahl an zu unterstützenden Szenarien nicht unterstützt. |
| params | Objekt | Nein | mbox-Parameter. Ein Objekt aus Schlüssel-Wert-Paaren mit der folgenden Struktur:<P>`{ "param1": "value1", "param2": "value2"}` |
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
>Wenn die Pflichtfelder nicht festgelegt sind, wird keine Anforderung ausgeführt und ein Fehler wird ausgegeben.
