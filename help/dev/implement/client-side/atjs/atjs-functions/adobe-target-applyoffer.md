---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, apply offer, at.js, features, function, $8
description: Verwenden Sie die Funktion [!UICONTROL adobe.target.applyOffer()] für die JavaScript-Bibliothek [!DNL Adobe Target] at.js , um den Antwortinhalt anzuwenden.
title: Wie verwende ich die Funktion "[!UICONTROL adobe.target.applyOffer()]"?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 69%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Diese Funktion dient zum Anwenden des Antwortinhalts mit [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` erfordert den Parameter `mbox`. Wurde kein Mbox-Name angegeben, tritt ein Fehler auf.

Der Optionsparameter ist obligatorisch und hat die folgende Struktur:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| mbox | Zeichenfolge | Ja | Name der Mbox<br />Bei at.js 1.3.0 (und höher) erzwingt Target die Verwendung des Mbox-Schlüssels. Dieser Schlüssel war früher erforderlich. Target erzwingt seine Verwendung jedoch nun, um sicherzustellen, dass Target ordnungsgemäß validiert ist und Kunden die Funktion richtig verwenden. |
| selector | Zeichenfolge oder DOM-Element | Nein | HTML-Element oder „selector“ in CSS wird dazu verwendet, das HTML-Element zu identifizieren, in dem die Angebotsinhalte platziert werden sollten. Wenn der Selektor nicht angegeben ist, geht Target davon aus, dass das HTML-Element HTML-HEAD verwenden sollte. |
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
