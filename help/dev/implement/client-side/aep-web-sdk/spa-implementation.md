---
title: Implementieren von Einzelseiten-Apps für den [!DNL Adobe Experience Platform Web SDK]
description: Erfahren Sie, wie Sie eine SPA-Implementierung (Single Page Application) von  [!DNL Adobe Experience Platform Web SDK]using [!DNL Target] erstellen.
keywords: Target;Adobe Target;XDM-Ansichten;Ansichten;Einzelseitenanwendungen;SPA;SPA-Lebenszyklus;Client-seitig;AB-Tests;AB;Erlebnis-Targeting;XT;VEC
feature: AEP Web SDK
exl-id: 17e71e47-c7cc-421a-bc9c-53f45f587449
TQID: https://experienceleague.adobe.com/Kp5fxEhLaXUNi6GOXXnET-1ueGQVLC0tPFhYzShk0cQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1836
ht-degree: 2%

---

# Implementieren von Einzelseiten-Apps

[!DNL Adobe Experience Platform Web SDK] bietet umfangreiche Funktionen, mit denen Ihr Unternehmen Personalisierungen auf Client-seitigen Technologien der nächsten Generation wie Single Page Applications (SPAs) durchführen kann.

Herkömmliche Websites verwendeten „Page-to-Page“-Navigationsmodelle, auch „Multi Page Applications“ genannt. In diesen Websites sind Designs eng mit URLs verknüpft. Das Wechseln zwischen Seiten erfordert das vollständige Laden der Seite.

Moderne Web-Anwendungen, wie z. B. Einzelseitenanwendungen, haben stattdessen ein Modell übernommen, das die schnelle Verwendung der Darstellung der Browser-Benutzeroberfläche unterstützt, die häufig unabhängig von Seitenneuladungen ist. Diese Erlebnisse werden durch Kundeninteraktionen wie Bildläufe, Klicks und Cursor-Bewegungen ausgelöst. Im Zuge der Weiterentwicklung der Paradigmen des modernen Internets funktioniert die Relevanz herkömmlicher generischer Ereignisse, wie z. B. des Seitenladevorgangs, für die Bereitstellung von Personalisierung und Experimenten nicht mehr.

![Diagramm, das den SPA-Lebenszyklus im Vergleich zum herkömmlichen Seitenlebenszyklus zeigt.](/help/dev/implement/client-side/aep-web-sdk/assets/spa-vs-traditional-lifecycle.png)

## Vorteile von [!DNL Experience Platform Web SDK] für SPAs

Die Verwendung von [!DNL Adobe Experience Platform Web SDK] für Single-Page-Anwendungen bietet folgende Vorteile:

* Möglichkeit zur Zwischenspeicherung aller Angebote beim Seitenladen, um mehrere Server-Aufrufe auf einen einzelnen Server-Aufruf zu reduzieren
* Verbessern Sie das Benutzererlebnis auf Ihrer Site, da Angebote sofort über den Cache angezeigt werden, ohne dass die durch herkömmliche Server-Aufrufe eingeführte Verzögerung eintritt.
* Eine einzelne Codezeile und ein einmaliges Entwicklersetup ermöglichen es Marketing-Experten, [!UICONTROL A/B-Test]- und [!UICONTROL Experience Targeting]-Aktivitäten über den [!UICONTROL Visual Experience Composer] (VEC) in Ihrer SPA zu erstellen und auszuführen.

## XDM-Ansichten und Single Page Applications

Der [!UICONTROL Adobe Target] VEC für SPAs nutzt ein Konzept namens [!UICONTROL Views]: eine logische Gruppe visueller Elemente, die zusammen ein SPA-Erlebnis bilden. Ein Single Page Application kann daher basierend auf Benutzerinteraktionen als Übergang durch Ansichten anstelle von URLs betrachtet werden. Eine [!UICONTROL Ansicht] kann in der Regel eine ganze Site oder gruppierte visuelle Elemente innerhalb einer Site darstellen.

Um näher zu erläutern, was Ansichten sind, wird im folgenden Beispiel eine hypothetische Online-E-Commerce-Site verwendet, die in implementiert ist, [!DNL React] Beispiele ([!UICONTROL ) ].

Nachdem Sie zur Startseite navigiert sind, fördert ein Hero-Bild einen Osterverkauf sowie die neuesten Produkte, die auf der Website verfügbar sind. In diesem Fall kann eine [!UICONTROL Ansicht] für den gesamten Startbildschirm definiert werden. Diese [!UICONTROL Ansicht] könnte einfach „Home“ genannt werden.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

Wenn der Kunde sich mehr für die Produkte interessiert, die das Unternehmen verkauft, entscheidet er sich, auf den Link **Produkte** zu klicken. Ähnlich wie bei der -Startseite kann die gesamte Produkt-Site als „Ansicht[!UICONTROL  definiert ]. Diese [!UICONTROL Ansicht] könnte „products-all“ genannt werden.

![Beispielbild einer Single Page Application in einem Browser-Fenster, in dem alle Produkte angezeigt werden.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Da eine [!UICONTROL Ansicht] als eine ganze Site oder eine Gruppe visueller Elemente auf einer Site definiert werden kann. Die vier auf der Produktseite angezeigten Produkte konnten gruppiert und als &quot;[!UICONTROL &quot; betrachtet ]. Diese Ansicht kann als „Produkte“ bezeichnet werden.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster mit angezeigten Beispielprodukten.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Wenn der Kunde auf die Schaltfläche **Mehr laden** klickt, um weitere Produkte auf der Website zu erkunden, ändert sich die Website-URL in diesem Fall nicht. Hier kann jedoch [!UICONTROL Ansicht] erstellt werden, um nur die zweite Zeile der angezeigten Produkte darzustellen. Der [!UICONTROL View]-Name könnte „products-page-2“ lauten.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster mit Beispielprodukten, die auf einer zusätzlichen Seite angezeigt werden.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

Der Kunde entscheidet sich für den Kauf einiger Produkte auf der Website und geht zum Checkout-Bildschirm über. Auf der Checkout-Website erhält der Kunde Optionen, um einen normalen Versand oder einen Expressversand auszuwählen. Eine [!UICONTROL Ansicht] kann eine beliebige Gruppe visueller Elemente auf einer Site sein, sodass eine [!UICONTROL Ansicht] für Versandvoreinstellungen erstellt und als „Versandvoreinstellungen“ bezeichnet werden kann.

![Beispielbild einer Single Page Application Checkout-Seite in einem Browser-Fenster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

Das Konzept [!UICONTROL Ansichten] kann weit über dieses Szenario hinaus erweitert werden. Diese Szenarien sind nur einige Beispiele für [!UICONTROL Ansichten] die auf einer Site definiert werden können.

## Implementieren von [!UICONTROL XDM-Ansichten]

[!UICONTROL XDM Views] können in [!DNL Target] genutzt werden, um Marketing-Experten die Durchführung von A/B- und XT-Tests an SPAs über den [!UICONTROL Visual Experience Composer] zu ermöglichen. Dies erfordert die Durchführung der folgenden Schritte, um eine einmalige Entwicklereinrichtung abzuschließen:

1. [Adobe Experience Platform Web SDK installieren](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
2. Bestimmen Sie alle [!UICONTROL XDM-]) in Ihrem Einzelseitenprogramm, die Sie personalisieren möchten.
3. Implementieren Sie nach der Definition der [!UICONTROL XDM-]) zur Bereitstellung von A/B- oder XT-VEC-Aktivitäten die `sendEvent()`-Funktion mit `renderDecisions` auf `true` und der entsprechenden [!UICONTROL XDM-Ansicht] in Ihrer Single Page Application. Die [!UICONTROL XDM-Ansicht] muss in `xdm.web.webPageDetails.viewName` übergeben werden. In diesem Schritt können Marketing-Fachleute den [!UICONTROL Visual Experience Composer] zum Starten von A/B- und XT-Tests für diese XDM-Dateien nutzen.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Beim ersten `sendEvent()`-Aufruf werden alle [!UICONTROL XDM-]) abgerufen und zwischengespeichert, die für den Endbenutzer gerendert werden sollen. Nachfolgende `sendEvent()` mit übergebenen [!UICONTROL XDM Views] werden aus dem Cache gelesen und ohne einen Server-Aufruf gerendert.

## Beispiele für `sendEvent()` Funktionen

In diesem Abschnitt werden drei Beispiele beschrieben, die zeigen, wie die `sendEvent()`-Funktion in React für eine hypothetische E-Commerce-SPA aufgerufen wird.

### Beispiel 1: A/B-Test-Startseite

Das Marketing-Team möchte A/B-Tests auf der gesamten Startseite durchführen.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-1.png)

Um A/B-Tests auf der gesamten Startseite durchzuführen, müssen `sendEvent()` aufgerufen werden, wobei der XDM-`viewName` auf `home` gesetzt sein muss:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Beispiel 2: Personalisierte Produkte

Das Marketing-Team möchte die zweite Produktreihe personalisieren, indem die Farbe des Preisschilds nach dem Klicken auf „Mehr laden **in Rot** wird.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster mit personalisierten Angeboten.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Beispiel 3: Voreinstellungen für den A/B-Test-Versand

Das Marketing-Team möchte einen A/B-Test durchführen, um zu sehen, ob die Farbe der Schaltfläche von Blau in Rot geändert werden soll, wenn **Express-Versand** ausgewählt ist. Das Team ist der Ansicht, dass diese Änderung die Konversionen steigern kann (anstatt die Schaltflächenfarbe für beide Bereitstellungsoptionen blau zu halten).

![Beispielbild einer Single Page Application in einem Browser-Fenster mit A/B-Tests.](/help/dev/implement/client-side/aep-web-sdk/assets/use-case-3.png)

Um Inhalte auf der Website je nach ausgewählter Versandvoreinstellung zu personalisieren, kann für [!UICONTROL  Versandvoreinstellung ]Ansicht“ erstellt werden. Wenn **Normaler Versand** ausgewählt ist, kann [!UICONTROL Ansicht] als „Checkout-Normal“ bezeichnet werden. Wenn **Express-Versand** ausgewählt ist, kann [!UICONTROL Ansicht] als „Checkout-Express“ bezeichnet werden.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Verwenden von [!UICONTROL Visual Experience Composer] für eine SPA

Wenn Sie mit der Definition Ihrer [!UICONTROL XDM-Ansichten] und der Implementierung von `sendEvent()` mit den [!UICONTROL XDM-Ansichten] fertig sind, kann der VEC diese [!UICONTROL Ansichten] erkennen und Benutzern ermöglichen, Aktionen und Änderungen für A/B- oder XT-Aktivitäten zu erstellen.

>[!NOTE]
>
>Um den VEC für Ihre SPA zu verwenden, müssen Sie entweder die [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder die [Chrome VEC Helper-Erweiterung](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) installieren und aktivieren.

### Bedienfeld [!UICONTROL Änderungen]

Das [!UICONTROL Änderungen] erfasst die Aktionen, die für eine bestimmte [!UICONTROL Ansicht] erstellt wurden. Alle Aktionen für eine [!UICONTROL Ansicht] sind unter dieser [!UICONTROL Ansicht] gruppiert.

### Aktionen

Durch Klicken auf eine Aktion wird das Element auf der Site hervorgehoben, auf die diese Aktion angewendet wird. Jede VEC-Aktion, die unter einer [!UICONTROL Ansicht] erstellt wird, weist die folgenden Symbole auf **Informationen**, **Bearbeiten**, **Klonen**, **Verschieben** und **Löschen**. Diese Symbole werden in der folgenden Tabelle detaillierter erläutert.

| Symbol | Beschreibung |
|---|---|
| Informationen | Zeigt die Details der Aktion an. |
| Bearbeiten | Ermöglicht die direkte Bearbeitung der Eigenschaften dieser Aktion. |
| Klonen | Klonen Sie die Aktion zu einer oder mehreren [!UICONTROL Ansichten], die im Bedienfeld [!UICONTROL Änderungen] vorhanden sind, oder zu einer oder mehreren [!UICONTROL Ansichten], die Sie im VEC durchsucht und aufgerufen haben. Die Aktion muss nicht unbedingt im Bedienfeld [!UICONTROL Änderungen] vorhanden sein.<br/><br/>**Hinweis:** Nachdem ein Klonvorgang durchgeführt wurde, müssen Sie über [!UICONTROL Durchsuchen] zum [!UICONTROL Anzeigen] im VEC navigieren, um zu sehen, ob die geklonte Aktion ein gültiger Vorgang war. Wenn die Aktion nicht auf die [!UICONTROL Ansicht] angewendet werden kann, wird ein Fehler angezeigt. |
| Verschieben | Verschiebt die Aktion in ein [!UICONTROL Seitenladeereignis] oder eine andere [!UICONTROL Ansicht] die bereits im [!UICONTROL Änderungen] vorhanden ist.<br/><br/>**Seitenladeereignis** Alle Aktionen, die dem Seitenladeereignis entsprechen, werden beim ersten Laden der Seite Ihrer Web-Anwendung angewendet. <br/><br/>**Hinweis:** Nachdem ein Verschiebevorgang durchgeführt wurde, müssen Sie über „Durchsuchen] zur [!UICONTROL Ansicht] [!UICONTROL  im VEC navigieren, um herauszufinden, ob der Verschiebevorgang gültig war. Wenn die Aktion nicht auf die [!UICONTROL Ansicht“ angewendet werden kann] wird ein Fehler angezeigt. |
| Löschen | Löscht die Aktion. |

## Beispiele für die Verwendung von VEC für SPAs

In diesem Abschnitt werden drei Beispiele für die Verwendung von [!UICONTROL Visual Experience Composer] zum Erstellen von Aktionen und Änderungen für A/B- oder XT-Aktivitäten beschrieben.

### Beispiel 1: Aktualisieren der Ansicht „Startseite“

Zuvor in diesem Artikel wurde eine [!UICONTROL Ansicht] mit dem Namen „Home“ für die gesamte Startseite definiert. Das Marketing-Team möchte nun die Ansicht „Startseite“ wie folgt aktualisieren:

* Ändern Sie die **Zum Warenkorb hinzufügen** und **Like**-Schaltflächen in einen helleren blauen Farbton. Diese Änderung sollte beim Laden der Seite vorgenommen werden, da dabei Komponenten der Kopfzeile geändert werden müssen.
* Ändern Sie die Bezeichnung **Neueste Produkte für 2026** in **Heißeste Produkte für**) und ändern Sie die Textfarbe in Lila.

Um diese Aktualisierungen in VEC vorzunehmen, wählen Sie **Erstellen** und wenden Sie diese Änderungen auf die Ansicht „Startseite“ an.

![Visual Experience Composer-Beispielseite.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Beispiel 2: Ändern von Produktbeschriftungen

Für die „products-page-2[!UICONTROL Ansicht] möchte das Marketing-Team die Beschriftung **Preis** in **Verkaufspreis** ändern und die Beschriftungsfarbe in Rot ändern.

Um diese Aktualisierungen in VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Wählen Sie **VEC** Durchsuchen) aus.
2. Wählen **Produkte** in der oberen Navigation der Site aus.
3. Wählen Sie **Mehr laden** einmal aus, um die zweite Zeile mit Produkten anzuzeigen.
4. Wählen Sie **VEC** Erstellen) aus.
5. Wenden Sie Aktionen an, um das Textfeld in **Verkaufspreis** und die Farbe in Rot zu ändern.

![Visual Experience Composer-Beispielseite mit Produktbeschriftungen.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Beispiel 3: Stil der Versandeinstellungen personalisieren

[!UICONTROL Ansichten] können auf einer granularen Ebene definiert werden, z. B. als Status oder eine Option über ein Optionsfeld. Zuvor in diesem Artikel [!UICONTROL Ansichten] wurden für Versandvoreinstellungen, „Checkout-Normal“ und „Checkout-Express“ definiert. Das Marketing-Team möchte die Farbe der Schaltfläche für die Ansicht „Checkout-Express“ in Rot ändern.

Um diese Aktualisierungen in VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Wählen Sie **VEC** Durchsuchen) aus.
2. Fügen Sie Produkte zum Warenkorb auf der Website hinzu.
3. Wählen Sie das Warenkorb -Symbol in der oberen rechten Ecke der Site aus.
4. Wählen Sie **Bestellung**.
5. Wählen Sie das **Express-Versand** unter **Versandeinstellungen** aus.
6. Wählen Sie **VEC** Erstellen) aus.
7. Ändern Sie die Farbe **Schaltfläche** Pay) in Rot.

>[!NOTE]
>
>Der „Checkout-Express“ [!UICONTROL Ansicht] wird erst im Bedienfeld [!UICONTROL Änderungen] angezeigt, wenn das Optionsfeld **Express-Versand** ausgewählt wird. Dies liegt daran, dass die `sendEvent()`-Funktion ausgeführt wird, wenn die Optionsschaltfläche **Express-Versand** ausgewählt ist. Daher ist dem VEC der „Checkout-Express“ ([!UICONTROL ) erst ], wenn die Optionsschaltfläche ausgewählt ist.

![Visual Experience Composer mit Auswahl der Versandvoreinstellungen.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
