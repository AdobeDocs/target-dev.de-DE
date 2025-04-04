---
keywords: globale mbox-Parameter, targetPageParams, Abfragezeichenfolge, Array, JSON, dtm
description: Erfahren Sie, wie Sie mit der [!UICONTROL targetPageParams]-Funktion zusätzliche Zielgruppen- oder Kontextinformationen an die  [!DNL Adobe Target] -globale Mbox übergeben.
title: Wie übergebe ich Parameter an eine globale Mbox?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 61%

---

# Übergeben von Parametern an eine globale Mbox

Die JavaScript `targetPageParams`-Funktion wird verwendet, um Parameter an die globale Mbox in [!DNL Adobe Target] zu übergeben. Dies ist in jedem Szenario erforderlich, in dem zusätzliche Zielgruppen-/Kontextinformationen an [!DNL Target] übergeben werden sollen.

Beispiel: Verwenden Sie in einer Recommendations-Aktivität die Parameter zur Darstellung des aktuellen Produkts oder der Kategorie, die angezeigt wird.

Der Code zum Aufrufen der JavaScript-Funktion muss vor der globalen Mbox auf der Seite stehen, unabhängig davon, ob die globale Mbox als Teil von at.js ausgelöst oder manuell in den Seiten-Code aufgenommen wird.

>[!NOTE]
>
>Wenn Sie Parameter zu allen Mboxes auf der Seite und nicht nur zur globalen Mbox hinzufügen möchten, verwenden Sie die Funktion [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md).

Um Parameter an `target-global-mbox` zu übergeben, können Sie die Funktion `targetPageParams()` auf eine der folgenden Arten verwenden:

* Als Array
* Als JSON-Objekt
* Als eine durch kaufmännisches Und getrennte Liste

Verwenden Sie diese drei Methoden, um zu prüfen, ob die Parameter korrekt übergeben wurden. Sie können die Übergabe der Parameter möglicherweise auch mit dem [Adobe Experience Cloud-Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html) prüfen.

Sie müssen die JavaScript-Funktion definieren, bevor Sie die globale Mbox zu der Seite hinzufügen. Der Name muss `targetPageParams` lauten.

## Abfragezeichenfolge

```
p1=v1&p2=v2&p3=hello%20world
```

* Name: `targetPageParams`
* Ausgabewert: mit „&amp;“ getrennte Parameter mit URL-codierten Parameterwerten.

  Beispiel:

  In diesem Beispiel hat p3 den Wert `hello world`, der URL-codiert ist.

Siehe folgenden Beispiel für Seiten-Code:

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

In diesem Beispiel werden die folgenden Daten an die Mbox-Edge gesendet:

* p1=v1
* p2=v2
* p3=hello world

## Array

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

Die Werte müssen nicht URL-codiert sein. Wenn beispielsweise ein Wert ein Leerzeichen enthält, dann muss dieses Leerzeichen nicht codiert werden.

In diesem Beispiel werden die folgenden Daten an die Mbox-Edge gesendet:

* a=1
* b=2
* c=hello world

## JSON

JSON ist eine leistungsstarke Methode zur Übergabe von Parametern. [!DNL Target] verwendet die JSON-Objektschlüssel, um komplizierte Strukturen in einfache Parameter zu reduzieren.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

Die Werte müssen nicht URL-codiert sein. Beispiel: Bei „San Francisco“ muss das Leerzeichen nicht codiert werden. Ein Leerzeichen genügt.

In diesem Beispiel werden die folgenden Daten an die Mbox-Edge gesendet:

* a=1
* b=2
* `profile.memberStatus`=Gold
* `profile.country.city`=San Francisco
