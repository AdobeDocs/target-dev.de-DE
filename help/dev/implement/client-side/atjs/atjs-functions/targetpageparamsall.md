---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, Seitenparameter, Seitenparameter, at.js, Funktionen, Funktion, targetPageParamsAll0
description: Verwenden Sie die Funktion [!UICONTROL targetPageParamsAll()] für die JavaScript-Bibliothek " [!DNL Adobe Target] .js“, um Parameter von außerhalb des Anforderungs-Codes an alle Mboxes anzuhängen.
title: Wie verwende ich die Funktion [!UICONTROL targetPageParamsAll()]?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
TQID: https://experienceleague.adobe.com/A2sZYp7CeE3-zGcqfbvgo32auAtXBKN0dYNa84grs1Q
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 171
ht-degree: 54%

---

# [!UICONTROL targetPageParamsAll()]

Mit dieser Methode können Sie Parameter von außerhalb des Anforderungscodes an alle Mboxes anfügen.

Dies ist sehr nützlich, wenn dieselbe Parameterkonfiguration für mehrere Mbox-Aufrufe verwendet werden soll. Sie muss vom Kunden definiert werden. Sie sollte ein Array von Parametern zurückgeben, die an alle Mbox-Aufrufe auf der Seite übergeben werden. Diese Funktion kann definiert werden, bevor at.js geladen wird, oder unter **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Bearbeiten]** > **[!UICONTROL Code-Einstellungen]** > **[!UICONTROL Bibliothekskopfzeile]**.

Sie können Parameter mithilfe der Funktion [!UICONTROL targetPageParamsAll() auf eine der folgenden Arten ] target-global-mbox übergeben:

* Als eine durch kaufmännisches Und getrennte Liste
* Als Array
* Als JSON-Objekt

## Beispiele

Durch kaufmännisches Und getrennte Liste (Werte müssen URL-codiert sein):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Array (Werte müssen nicht URL-codiert sein):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON (Werte müssen nicht URL-codiert sein):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```

