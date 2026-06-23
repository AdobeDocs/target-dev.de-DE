---
keywords: adobe.target.applyOffer, applyOffer, applyOffer, apply offer, at.js, Funktionen, Funktion, $8
description: Verwenden Sie die Funktion [!UICONTROL adobe.target.applyOffer()] für die JavaScript-Bibliothek " [!DNL Adobe Target] .js“, um den Antwortinhalt anzuwenden.
title: Wie verwende ich die Funktion [!UICONTROL adobe.target.applyOffer()]?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
TQID: https://experienceleague.adobe.com/lrjsIl-gKu1SnrZapxYcoDObvUCGG2ht58QtWbQkYts
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 68%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Diese Funktion dient zum Anwenden des Antwortinhalts auf [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` erfordert den Parameter `mbox`. Wurde kein Mbox-Name angegeben, tritt ein Fehler auf.

Der Optionsparameter ist obligatorisch und hat die folgende Struktur:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| mbox | Zeichenfolge | Ja | Name der Mbox<br />Bei at.js 1.3.0 (und höher) erzwingt Target die Verwendung des Mbox-Schlüssels. Dieser Schlüssel war früher erforderlich. Target erzwingt seine Verwendung jedoch nun, um sicherzustellen, dass Target ordnungsgemäß validiert ist und Kunden die Funktion richtig verwenden. |
| selector | Zeichenfolge oder DOM-Element | Nein | HTML-Element oder „selector“ in CSS wird dazu verwendet, das HTML-Element zu identifizieren, in dem die Angebotsinhalte platziert werden sollten. Wenn kein Selektor bereitgestellt wird, geht Target davon aus, dass das HTML-Element HTML HEAD verwenden sollte. |
| Angebot | Array | Ja | Eine Reihe von Aktionen, die auf das Element angewendet werden sollen |

## Beispiel

Das folgende Beispiel demonstriert, wie `[!UICONTROL getOffer]` und `[!UICONTROL applyOffer]` gemeinsam genutzt werden:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```

