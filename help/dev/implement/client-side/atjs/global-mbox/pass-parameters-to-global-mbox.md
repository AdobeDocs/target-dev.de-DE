---
keywords: globale mbox-Parameter, targetPageParams, Abfragezeichenfolge, Array, JSON, dtm
description: Erfahren Sie, wie Sie mit der [!UICONTROL targetPageParams]-Funktion zusätzliche Zielgruppen- oder Kontextinformationen an die  [!DNL Adobe Target] -globale Mbox übergeben.
title: Wie übergebe ich Parameter an eine globale Mbox?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
TQID: https://experienceleague.adobe.com/MRdqU23ARg1E-gf8QDbXOpaVJWd9Fx1pqJ4QXjsBdtA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 378
ht-degree: 60%

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
