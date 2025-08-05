---
title: Implementieren von Einzelseiten-Apps für den [!DNL Adobe Experience Platform Web SDK]
description: Erfahren Sie, wie Sie eine SPA-Implementierung (Single Page Application) von  [!DNL Adobe Experience Platform Web SDK]using [!DNL Target] erstellen.
keywords: Target;Adobe Target;XDM-Ansichten;Ansichten;Einzelseitenanwendungen;SPA;SPA-Lebenszyklus;Client-seitig;AB-Tests;AB;Erlebnis-Targeting;XT;VEC
feature: AEP Web SDK
source-git-commit: 9a2c35b2d150638fbda00be866f84d2a6faa4300
workflow-type: tm+mt
source-wordcount: '1680'
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
* Eine einzige Codezeile und ein einmaliges Entwicklersetup ermöglichen es Marketing-Experten, [!UICONTROL A/B Test]- und [!UICONTROL Experience Targeting]-Aktivitäten über den [!UICONTROL Visual Experience Composer] (VEC) in Ihrer SPA zu erstellen und auszuführen.

## XDM-Ansichten und Single Page Applications

Der [!UICONTROL Adobe Target] VEC für SPAs nutzt ein Konzept namens [!UICONTROL Views]: eine logische Gruppe visueller Elemente, die zusammen ein SPA-Erlebnis bilden. Ein Single Page Application kann daher basierend auf Benutzerinteraktionen als Übergang durch Ansichten anstelle von URLs betrachtet werden. Ein [!UICONTROL View] kann in der Regel eine ganze Site oder gruppierte visuelle Elemente innerhalb einer Site darstellen.

Um näher zu erläutern, was Ansichten sind, wird im folgenden Beispiel eine hypothetische Online-E-Commerce-Site verwendet, die in implementiert ist, [!DNL React] Beispiel-[!UICONTROL Views] zu untersuchen.

Nachdem Sie zur Startseite navigiert sind, fördert ein Hero-Bild einen Osterverkauf sowie die neuesten Produkte, die auf der Website verfügbar sind. In diesem Fall kann eine [!UICONTROL View] für den gesamten Startbildschirm definiert werden. Diese [!UICONTROL View] könnte man einfach „Heimat“ nennen.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-views.png)

Wenn der Kunde sich mehr für die Produkte interessiert, die das Unternehmen verkauft, entscheidet er sich, auf den Link **Produkte** zu klicken. Ähnlich wie bei der -Startseite kann die gesamte Produkt-Site als [!UICONTROL View] definiert werden. Dieses [!UICONTROL View] könnte „products-all“ genannt werden.

![Beispielbild einer Single Page Application in einem Browser-Fenster, in dem alle Produkte angezeigt werden.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products-all.png)

Da ein [!UICONTROL View] als eine ganze Site oder als eine Gruppe visueller Elemente auf einer Site definiert werden kann. Die vier auf der Produktseite aufgeführten Produkte konnten gruppiert und als [!UICONTROL View] betrachtet werden. Diese Ansicht kann als „Produkte“ bezeichnet werden.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster mit angezeigten Beispielprodukten.](/help/dev/implement/client-side/aep-web-sdk/assets/example-products.png)

Wenn der Kunde auf die Schaltfläche **Mehr laden** klickt, um weitere Produkte auf der Website zu erkunden, ändert sich die Website-URL in diesem Fall nicht. Hier kann jedoch eine [!UICONTROL View] erstellt werden, die nur die zweite Zeile der angezeigten Produkte darstellt. Der [!UICONTROL View] könnte „products-page-2“ lauten.

![Beispielbild eines Einzelseiten-Programms in einem Browser-Fenster mit Beispielprodukten, die auf einer zusätzlichen Seite angezeigt werden.](/help/dev/implement/client-side/aep-web-sdk/assets/example-load-more.png)

Der Kunde entscheidet sich für den Kauf einiger Produkte auf der Website und geht zum Checkout-Bildschirm über. Auf der Checkout-Website erhält der Kunde Optionen, um einen normalen Versand oder einen Expressversand auszuwählen. Eine [!UICONTROL View] kann eine beliebige Gruppe visueller Elemente auf einer Site sein, sodass ein [!UICONTROL View] für Versandvoreinstellungen erstellt und als „Versandvoreinstellungen“ bezeichnet werden kann.

![Beispielbild einer Single Page Application Checkout-Seite in einem Browser-Fenster.](/help/dev/implement/client-side/aep-web-sdk/assets/example-check-out.png)

Das Konzept der [!UICONTROL Views] kann weit über dieses Szenario hinaus erweitert werden. Diese Szenarien sind nur einige Beispiele für [!UICONTROL Views], die auf einer Site definiert werden können.

## Implementieren von [!UICONTROL XDM Views]

[!UICONTROL XDM Views] können genutzt werden, [!DNL Target] es Marketing-Experten zu ermöglichen, A/B- und XT-Tests über die -[!UICONTROL Visual Experience Composer] auf SPAs durchzuführen. Dies erfordert die Durchführung der folgenden Schritte, um eine einmalige Entwicklereinrichtung abzuschließen:

1. [Adobe Experience Platform Web SDK installieren](https://experienceleague.adobe.com/de/docs/experience-platform/web-sdk/install/overview).
2. Bestimmen Sie alle [!UICONTROL XDM Views] in Ihrem Einzelseitenprogramm, die Sie personalisieren möchten.
3. Implementieren Sie nach der Definition der [!UICONTROL XDM Views] für die Bereitstellung von A/B- oder XT-VEC-Aktivitäten die `sendEvent()`, wobei `renderDecisions` auf `true` und die entsprechenden [!UICONTROL XDM View] in Ihrer Single Page Application festgelegt sind. Die [!UICONTROL XDM View] muss in `xdm.web.webPageDetails.viewName` übergeben werden. In diesem Schritt können Marketing-Fachleute die [!UICONTROL Visual Experience Composer] zum Starten von A/B- und XT-Tests für diese XDM nutzen.

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
>Beim ersten `sendEvent()`-Aufruf werden alle [!UICONTROL XDM Views] abgerufen und zwischengespeichert, die für den Endbenutzer gerendert werden sollen. Nachfolgende `sendEvent()` mit übergebenen [!UICONTROL XDM Views] werden aus dem Cache gelesen und ohne einen Server-Aufruf gerendert.

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

Um Inhalte auf der Website je nach ausgewählter Versandvoreinstellung zu personalisieren, kann für jede Versandvoreinstellung eine [!UICONTROL View] erstellt werden. Wenn **Normaler Versand** ausgewählt ist, kann der [!UICONTROL View] als „Checkout-Normal“ bezeichnet werden. Wenn **Express-Versand** ausgewählt ist, kann der [!UICONTROL View] als „Checkout-Express“ bezeichnet werden.

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

## Verwenden der [!UICONTROL Visual Experience Composer] für eine SPA

Wenn Sie mit der Definition Ihrer [!UICONTROL XDM Views] und der Implementierung von `sendEvent()` mit den übergebenen [!UICONTROL XDM Views] fertig sind, kann der VEC diese [!UICONTROL Views] erkennen und Benutzern ermöglichen, Aktionen und Änderungen für A/B- oder XT-Aktivitäten zu erstellen.

>[!NOTE]
>
>Um den VEC für Ihre SPA zu verwenden, müssen Sie entweder die [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder die [Chrome VEC Helper-Erweiterung](https://experienceleague.adobe.com/de/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) installieren und aktivieren.

### [!UICONTROL Modifications]

Das Bedienfeld [!UICONTROL Modifications] erfasst die für eine bestimmte [!UICONTROL View] erstellten Aktionen. Alle Aktionen für eine [!UICONTROL View] werden unter diesem [!UICONTROL View] gruppiert.

### Aktionen

Durch Klicken auf eine Aktion wird das Element auf der Site hervorgehoben, auf die diese Aktion angewendet wird. Jede VEC-Aktion, die unter einem [!UICONTROL View] erstellt wird, weist die folgenden Symbole auf **Informationen**, **Bearbeiten**, **Klonen**, **Verschieben** und **Löschen**. Diese Symbole werden in der folgenden Tabelle detaillierter erläutert.

| Symbol | Beschreibung |
|---|---|
| Informationen | Zeigt die Details der Aktion an. |
| Bearbeiten | Ermöglicht die direkte Bearbeitung der Eigenschaften dieser Aktion. |
| Klonen | Klonen Sie die Aktion zu einem oder mehreren [!UICONTROL Views] im [!UICONTROL Modifications] oder zu einem oder mehreren [!UICONTROL Views], die Sie im VEC durchsucht und aufgerufen haben. Die Aktion muss nicht unbedingt im [!UICONTROL Modifications] vorhanden sein.<br/><br/>**Hinweis:** Nachdem ein Klonvorgang durchgeführt wurde, müssen Sie über [!UICONTROL View] zur [!UICONTROL Browse] in VEC navigieren, um zu sehen, ob die geklonte Aktion ein gültiger Vorgang war. Wenn die Aktion nicht auf die [!UICONTROL View] angewendet werden kann, wird ein Fehler angezeigt. |
| Verschieben  | Verschiebt die Aktion in eine [!UICONTROL Page Load Event] oder eine andere [!UICONTROL View], die bereits im [!UICONTROL Modifications] vorhanden ist.<br/><br/>**Seitenladeereignis** Alle Aktionen, die dem Seitenladeereignis entsprechen, werden beim ersten Laden der Seite Ihrer Web-Anwendung angewendet. <br/><br/>**Hinweis:** Nachdem ein Verschiebevorgang durchgeführt wurde, müssen Sie über [!UICONTROL View] zum [!UICONTROL Browse] in VEC navigieren, um zu sehen, ob der Verschiebevorgang gültig war. Wenn die Aktion nicht auf die [!UICONTROL View] angewendet werden kann, wird ein Fehler angezeigt. |
| Löschen | Löscht die Aktion. |

## Beispiele für die Verwendung von VEC für SPAs

In diesem Abschnitt werden drei Beispiele für die Verwendung der [!UICONTROL Visual Experience Composer] zum Erstellen von Aktionen und Änderungen für A/B- oder XT-Aktivitäten beschrieben.

### Beispiel 1: Aktualisieren der Ansicht „Startseite“

Zuvor in diesem Artikel wurde ein [!UICONTROL View] mit dem Namen „Home“ für die gesamte Startseite definiert. Das Marketing-Team möchte nun die Ansicht „Startseite“ wie folgt aktualisieren:

* Ändern Sie die **Zum Warenkorb hinzufügen** und **Like**-Schaltflächen in einen helleren blauen Farbton. Diese Änderung sollte beim Laden der Seite vorgenommen werden, da dabei Komponenten der Kopfzeile geändert werden müssen.
* Ändern Sie die Bezeichnung **Neueste Produkte für 2026** in **Heißeste Produkte für**) und ändern Sie die Textfarbe in Lila.

Um diese Aktualisierungen in VEC vorzunehmen, wählen Sie **Erstellen** und wenden Sie diese Änderungen auf die Ansicht „Startseite“ an.

![Visual Experience Composer-Beispielseite.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-home.png)

### Beispiel 2: Ändern von Produktbeschriftungen

Für die [!UICONTROL View] „products-page-2“ möchte das Marketing-Team die Beschriftung **Preis** in **Verkaufspreis** ändern und die Beschriftungsfarbe in Rot ändern.

Um diese Aktualisierungen in VEC vorzunehmen, sind die folgenden Schritte erforderlich:

1. Wählen Sie **VEC** Durchsuchen) aus.
2. Wählen **Produkte** in der oberen Navigation der Site aus.
3. Wählen Sie **Mehr laden** einmal aus, um die zweite Zeile mit Produkten anzuzeigen.
4. Wählen Sie **VEC** Erstellen) aus.
5. Wenden Sie Aktionen an, um das Textfeld in **Verkaufspreis** und die Farbe in Rot zu ändern.

![Visual Experience Composer-Beispielseite mit Produktbeschriftungen.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-products-page-2.png)

### Beispiel 3: Stil der Versandeinstellungen personalisieren

[!UICONTROL Views] können auf einer granularen Ebene definiert werden, z. B. als Status oder eine Option über ein Optionsfeld. Zuvor in diesem Artikel wurden [!UICONTROL Views] für Versandvoreinstellungen, „Checkout-Normal“ und „Checkout-Express“ definiert. Das Marketing-Team möchte die Farbe der Schaltfläche für die Ansicht „Checkout-Express“ in Rot ändern.

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
>Die [!UICONTROL View] „Checkout-Express“ wird erst dann im [!UICONTROL Modifications] angezeigt, wenn das Optionsfeld **Express-Versand** ausgewählt ist. Dies liegt daran, dass die Funktion `sendEvent()` ausgeführt wird, wenn die Optionsschaltfläche **Express-Versand** ausgewählt ist. Daher ist dem VEC die [!UICONTROL View] „Checkout-Express“ erst bekannt, wenn die Optionsschaltfläche ausgewählt ist.

![Visual Experience Composer mit Auswahl der Versandvoreinstellungen.](/help/dev/implement/client-side/aep-web-sdk/assets/vec-delivery-preference.png)
