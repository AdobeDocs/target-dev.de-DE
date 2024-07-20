---
keywords: adobe.target.getOffer, getOffer, getoffer, get offer, at.js, Funktionen, Funktion, $8
description: Verwenden Sie die Funktion "[!UICONTROL adobe.target.getOffer()]"und die zugehörigen Optionen für die Bibliothek " [!DNL Adobe Target] at.js", um Anforderungen auszulösen, um ein [!DNL Target] Angebot zu erhalten.
title: Wie verwende ich die Funktion "[!UICONTROL adobe.target.getOffer()]"?
feature: at.js
exl-id: 7b917d42-06e8-4838-a09d-0c4872c9beaa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 81%

---

# [!DNL adobe.target.getOffer(options)]

Diese Funktion löst eine Anfrage zum Abrufen eines [!DNL Target] -Angebots aus.

Verwenden Sie sie mit `[!UICONTROL adobe.target.applyOffer()]`, um die Antwort zu verarbeiten, oder verwenden Sie Ihre eigene Methode für die Verarbeitung von „success“. Der Optionsparameter ist obligatorisch und hat die folgende Struktur:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| mbox | Zeichenfolge | Ja | Name der Mbox |
| params | Objekt | Nein | Mbox-Parameter Ein Objekt aus Schlüssel-Wert-Paaren mit der folgenden Struktur:<P>`{ "param1": "value1", "param2": "value2"}` |
| success | Funktion | Ja | Rückruf wird ausgeführt, wenn eine Antwort vom Server eingegangen ist. Die Rückruffunktion „success“ erhält einen einzelnen Parameter, der ein Array von Angebotsobjekten enthält. Im Folgenden finden Sie ein Beispiel für einen Rückruf bei einem Erfolg:<P>`function handleSuccess(response){......}`<P>Details finden Sie unten unter „Antworten“. |
| error | Funktion | Ja | Auszuführender Rückruf bei Eingang eines Fehlers Es gibt einige Fälle, die als fehlerhaft angesehen werden:<ul><li>Der HTTP-Status-Code weicht von „200 OK“ ab.</li><li>Die Antwort kann nicht analysiert werden. Dies kann zum Beispiel bei schlecht programmiertem JSON-Code oder HTML- statt JSON-Code auftreten.</li><li>Die Antwort enthält den Schlüssel „error“. Dies kann zum Beispiel der Fall sein, wenn eine Ausnahme auf dem Edgeserver auftritt und eine Anforderung nicht richtig verarbeitet werden konnte. Ein Fehler tritt auch dann auf, wenn eine Mbox blockiert ist und dafür keine Inhalte abgerufen werden konnten und so weiter. Die Rückruffunktion „error“ erhält zwei Parameter: „status“ und „error“. Beispiel für einen Fehler-Rückruf: `function handleError(status, error){......}`</li></ul>Details finden Sie unten unter „Fehlermeldungen“. |
| Zeitüberschreitung | Nummer | Nein | Zeitüberschreitung in Millisekunden Wird kein Wert festgelegt, kommt der Standardwert für die Zeitüberschreitung in at.js zum Einsatz.<P>Der standardmäßige Timeout kann über die [!DNL Target] -Benutzeroberfläche unter [!UICONTROL Administration] > [!UICONTROL Implementation] festgelegt werden. |

## Beispiele

Hinzufügen von Parametern mit [!UICONTROL getOffer()] und Verwendung von [!UICONTROL applyOffer()] für die Erfolgsbehandlung:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Hinzufügen von Parametern und Profilparametern mit [!UICONTROL getOffer()] und Verwendung von [!UICONTROL applyOffer()] für die Erfolgsbehandlung:

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2, 
     "profile.age": 27, 
     "profile.gender": "male" 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

Verwenden von benutzerdefiniertem Timeout und benutzerdefinierter Erfolgsbehandlung mit [!UICONTROL getOffer()]:

„YOUR_OWN_CUSTOM_HANDLING_FUNCTION“ ist ein Platzhalter für eine Funktion, die der Kunde definieren würde.

```javascript {line-numbers="true"}
adobe.target.getOffer({     
  "mbox": "target-global-mbox",   
  "success": function(offer) { 
    YOUR_OWN_CUSTOM_HANDLING_FUNCTION(offer);   
  }, 
  "error": function(status, error) {                 
    console.log('Error', status, error);   
  },   
  "timeout": 2000 
});
```

## Antworten

Der Antwortparameter, der an die Rückruffunktion „success“ weitergegeben wurde, ist eine Reihe von Aktionen. Eine Aktion ist ein Objekt, das für gewöhnlich das folgende Format hat:

| Name | Typ | Beschreibung |
|--- |--- |--- |
| Aktion | Zeichenfolge | Art der Aktion, die auf das identifizierte Element angewendet werden soll |
| selector | Zeichenfolge | Repräsentiert einen Sizzle-Selector |
| cssSelector | Zeichenfolge | DOM-nativer Selektor, für das Vorab-Ausblenden von Elementen verwendet |
| content | Zeichenfolge | Der Inhalt, der auf das identifizierte Element angewendet werden soll |

## Beispiel

```javascript {line-numbers="true"}
{ 
    "sessionId": "1444512212156-384616", 
    "tntId": "1444512212156-384616.17_35", 
    "offers": [{ 
        "plugins": ["<script type=\"text/javascript\">\r\n/*mboxHighlight+ (1of2) v1 ==> Response Plugin*/\r\nwindow.ttMETA=(typeof(window.ttMETA)!='undefined')?window.ttMETA:[];window.ttMETA.push({'mbox':'target-global-mbox','campaign':'at: redirect ootb','experience':'Experience B','offer':'/at_redirect_ootb/experiences/1/pages/0/1442082890250'});window.ttMBX=function(x){var mbxList=[];for(i=0;i<ttMETA.length;i++){if(ttMETA[i].mbox==x.getName()){mbxList.push(ttMETA[i])}}return mbxList[x.getId()]}\r\n</script>"], 
        "actions": { 
            "content": [{ 
                "passMboxSession": false, 
                "selector": "body", 
                "action": "redirect", 
                "url": "https://example.com/04.html", 
                "includeAllUrlParameters": true 
            }] 
        } 
    }] 
}
```

## Fehlermeldungen

Die an den Rückruf mit Fehler übergebenen Parameter „status“ und „error“ haben das folgende Format:

| Name | Typ | Beschreibung |
|--- |--- |--- |
| status | Zeichenfolge | Stellt den Fehlerstatus dar Dieser Parameter kann die folgenden Werte annehmen:<ul><li>timeout: Gibt an, dass die Anfrage abgelaufen ist.</li><li>parseerror: Gibt an, dass die Antwort nicht analysiert werden konnte, zum Beispiel wenn HTML-Code oder Klartext statt JSON gesendet wurde.</li><li>error: Gibt an, dass ein allgemeines Problem aufgetreten ist, etwa wenn wir einen HTTP-Status erhalten, der nicht „200 OK“ lautet.</li></ul> |
| error | Zeichenfolge | Enthält zusätzliche Daten wie zum Beispiel die Ausnahmemeldung oder andere Informationen, die bei der Fehlerhebung hilfreich sein könnten |
