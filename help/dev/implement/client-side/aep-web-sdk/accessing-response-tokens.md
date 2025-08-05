---
title: Zugreifen auf Antwort-Token mithilfe der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem auf Antwort-Token  [!DNL Adobe Experience Platform Web SDK].
keywords: Personalisierung;Target;Adobe Target;renderDecisions;sendEvent;Entscheidungsumfänge;result.decisions,Response Token;
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Zugriff auf Antwort-Token

Personalization-Inhalte, die von [!DNL Adobe Target] zurückgegeben werden[ umfassen ](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)Antwort-Token), die Details zur Aktivität, zum Angebot, zum Erlebnis, zum Benutzerprofil, zu geografischen Informationen und mehr sind. Diese Details können für Drittanbieter-Tools freigegeben oder zum Debugging verwendet werden. Antwort-Token können in der [!DNL Target]-Benutzeroberfläche konfiguriert werden.

Um auf Personalisierungsinhalte zuzugreifen, stellen Sie beim Senden eines Ereignisses eine Rückruffunktion bereit. Dieser Rückruf wird aufgerufen, nachdem die SDK eine erfolgreiche Antwort vom Server erhalten hat. Ihr Callback wird als `result`-Objekt bereitgestellt, das eine `propositions`-Eigenschaft enthalten kann, die alle zurückgegebenen Personalisierungsinhalte enthält. Nachfolgend finden Sie ein Beispiel für die Bereitstellung einer Rückruffunktion.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In diesem Beispiel ist `result.propositions`, falls vorhanden, ein Array mit Personalisierungsvorschlägen im Zusammenhang mit dem Ereignis. Weitere Informationen [ Inhalt von ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) finden `result.propositions.` unter „Rendern von Personalisierungsinhalten“

Angenommen, Sie möchten alle Aktivitätsnamen aus allen Vorschlägen erfassen, die automatisch von Web SDK gerendert wurden, und sie in ein einziges Array pushen. Sie können dann das einzelne Array an einen Drittanbieter senden. In diesem Fall:

1. Extrahieren von Vorschlägen aus dem `result`.
1. Durchlaufen aller Vorschläge
1. Stellen Sie fest, ob der SDK den Vorschlag gerendert hat.
1. Wenn ja, durchlaufen Sie alle Elemente im Vorschlag.
1. Rufen Sie den Aktivitätsnamen aus der `meta`-Eigenschaft ab, bei der es sich um ein Objekt mit Antwort-Token handelt.
1. Pushen Sie den Aktivitätsnamen in ein Array.
1. Senden Sie die Aktivitätsnamen an eine Drittpartei.

Ihr Code würde wie folgt aussehen:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
