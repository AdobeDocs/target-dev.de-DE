---
title: Verwenden  [!DNL Adobe Target] with [!DNL Web SDK]  für die Personalisierung.
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem  [!DNL Experience Platform Web SDK] using [!DNL Adobe Target] rendern.
feature: AEP Web SDK
source-git-commit: 1fe6adc25604612ed9fa090f1f68c18b9c0bdf63
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 5%

---

# [!DNL Adobe Target] und [!DNL Web SDK] für Personalisierung verwenden

[!DNL Adobe Experience Platform] [!DNL Web SDK] können personalisierte Erlebnisse bereitstellen und rendern, die in [!DNL Adobe Target] für den Web-Kanal verwaltet werden. Sie können einen WYSIWYG-Editor namens [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Ihre Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

>[!IMPORTANT]
>
>Erfahren Sie im Tutorial [!DNL Target]Migrieren von Target von at.js 2.x zu Experience Platform Web SDK&quot;, wie Sie Ihre [!DNL Experience Platform Web SDK]-Implementierung nach [ ](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=de).
>
>Erfahren Sie im Tutorial zur erstmaligen Implementierung von [!DNL Target] mit [Adobe Experience Cloud mit Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) . Spezifische Informationen zu [!DNL Target] finden Sie im Tutorial-Abschnitt [Einrichten von Target mit Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

Die folgenden Funktionen wurden getestet und werden derzeit in [!DNL Target] unterstützt:

* [A/B-Tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T Impression- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Experience Targeting-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivarianz-Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Berichte zu nativen Target-Impressionen und -Konversionen](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-Unterstützung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK]

Das folgende Diagramm hilft Ihnen, den Workflow von [!DNL Target] und [!DNL Web SDK] Edge Decisioning zu verstehen.

![Abbildung der Adobe Target-Edge-Entscheidungsfindung mit Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/assets/target-platform-web-sdk-new.png)

| Aufruf | Details |
| --- | --- |
| 1 | Das Gerät lädt die [!DNL Web SDK]. Der [!DNL Web SDK] sendet eine Anfrage mit XDM-Daten, der Datenstrom-Umgebungs-ID, den übergebenen Parametern und der Kunden-ID (optional) an die Edge Network. Seite (oder Container) ist vorab ausgeblendet. |
| 2 | Der Edge Network sendet die Anfrage an die Edge-Services, um sie mit der Besucher-ID, dem Einverständnis und anderen Besucherkontextinformationen wie Geolokalisierung und gerätefreundlichen Namen anzureichern. |
| 3 | Der Edge Network sendet die angereicherte Personalisierungsanfrage mit der Besucher-ID und den übergebenen Parametern an den [!DNL Target] Edge. |
| 4 | Profilskripte werden ausgeführt und fließen dann in [!DNL Target] Profilspeicher ein. Der Profilspeicher ruft Segmente aus dem [!UICONTROL Audience Library] ab (z. B. freigegebene Segmente aus [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] und dem [!DNL Adobe Experience Platform]). |
| 5 | Basierend auf URL-Anforderungsparametern und Profildaten bestimmt [!DNL Target], welche Aktivitäten und Erlebnisse für den Besucher bzw. die Besucherin in der aktuellen Seitenansicht und für zukünftige vorab abgerufene Ansichten angezeigt werden sollen. [!DNL Target] sendet dies dann zurück an die Edge Network. |
| 6 | a. Der Edge Network sendet die Personalisierungsantwort zurück an die Seite, wobei optional Profilwerte für die zusätzliche Personalisierung enthalten sind. Personalisierte Inhalte auf der aktuellen Seite werden so schnell wie möglich ohne Flackern der Standardinhalte angezeigt.<br> B. Personalisierte Inhalte für Ansichten, die als Ergebnis von Benutzeraktionen in einer Einzelseiten-App (SPA) angezeigt werden, werden zwischengespeichert, sodass sie sofort ohne zusätzlichen Server-Aufruf angewendet werden können, wenn die Ansichten ausgelöst werden. <br>c. Die Edge Network sendet die Besucher-ID und andere Werte in Cookies, z. B. Einverständnis, Sitzungs-ID, Identität, Cookie-Prüfung, Personalisierung. |
| 7 | Web SDK sendet die Benachrichtigung vom Gerät an Edge Network. |
| 8 | Edge Network leitet [!UICONTROL Analytics for Target] (A4T)-Details (Aktivitäts-, Erlebnis- und Konversionsmetadaten) an [!DNL Analytics] Edge weiter. |

## Aktivieren von [!DNL Adobe Target]

Gehen Sie wie folgt vor, um [!DNL Target] zu aktivieren:

1. Aktivieren Sie [!DNL Target] in Ihrem [Datenstrom](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) mit dem entsprechenden Client-Code.
1. Fügen Sie den Ereignissen die Option `renderDecisions` hinzu.

Anschließend können Sie optional auch die folgenden Optionen hinzufügen:

* **`decisionScopes`**: Rufen Sie bestimmte Aktivitäten ab (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* **[Ausschnitt vorab ausblenden](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/manage-flicker)**: Blendet nur bestimmte Bereiche der Seite aus.

## Verwenden des [!UICONTROL Adobe Target] VEC

Um VEC mit einer [!DNL Web SDK] Implementierung zu verwenden, installieren und aktivieren Sie entweder die [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder die VEC Helper-Erweiterung {3[Chrome).](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension)

Weitere Informationen finden Sie unter [Visual Experience Composer Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) im *Adobe Target-Handbuch*.

## Rendern von personalisierten Inhalten

Weitere Informationen [ Sie unter ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content) von Personalisierungsinhalten .

## Zielgruppen in XDM

Beim Definieren von Zielgruppen für die [!DNL Target]-Aktivitäten, die über die [!DNL Web SDK] bereitgestellt werden[ muss ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)XDM) definiert und verwendet werden. Nachdem Sie XDM-Schemata, Klassen und Schemafeldgruppen definiert haben, können Sie eine [!DNL Target] Zielgruppenregel erstellen, die durch XDM-Daten für das Targeting definiert wird. In [!DNL Target] werden XDM-Daten in der [!UICONTROL Audience Builder] als benutzerdefinierter Parameter angezeigt. Das XDM wird mit Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie über [!DNL Target] Aktivitäten mit vordefinierten Zielgruppen verfügen, die benutzerdefinierte Parameter oder ein Benutzerprofil verwenden, werden diese nicht ordnungsgemäß über die SDK bereitgestellt. Anstatt benutzerdefinierte Parameter oder das Benutzerprofil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch vordefinierte Zielgruppen-Targeting-Felder, die über die [!DNL Web SDK] unterstützt werden und kein XDM erfordern. Diese Felder sind in der [!DNL Target]-Benutzeroberfläche verfügbar, die kein XDM erfordern:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Betriebssystem
* Seiten der Site
* Browser
* Traffic-Quelle
* Zeitrahmen

Weitere Informationen finden Sie unter [Kategorien für Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) im *Adobe Target-Handbuch*.

### Antwort-Token

Antwort-Token werden verwendet, um Metadaten an Dritte wie Google oder Facebook zu senden. Antwort-Token werden zurückgegeben
Im `meta` Feld unter `propositions` > `items`.

Im Folgenden finden Sie ein Beispiel:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Um die Antwort-Token zu erfassen, müssen Sie `alloy.sendEvent` Versprechen abonnieren, `propositions` durchlaufen und die Details aus `items` -> `meta` extrahieren.

Jeder `proposition` verfügt über ein `renderAttempted` boolesches Feld, das angibt, ob der `proposition` gerendert wurde oder nicht. Siehe folgendes Beispiel:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Wenn die automatische Wiedergabe aktiviert ist, enthält das Vorschläge-Array Folgendes:

#### Beim Laden der Seite:

* Auf dem formularbasierten Composer basierende `propositions` mit `renderAttempted` Flag, das auf `false` gesetzt ist
* Auf Visual Experience Composer basierende Vorschläge mit `renderAttempted` Markierung `true`
* Auf Visual Experience Composer basierende Vorschläge für eine Einzelseiten-Programmansicht mit `renderAttempted` Markierung `true`

#### Bei Ansicht - Änderung (für Ansichten im Cache):

* Auf Visual Experience Composer basierende Vorschläge für eine Einzelseiten-Programmansicht mit `renderAttempted` Markierung `true`

Wenn die automatische Wiedergabe deaktiviert ist, enthält das Vorschläge-Array Folgendes:

#### Beim Laden der Seite:

* [!DNL Form-based Composer]-basierte `propositions` mit `renderAttempted` Markierung auf `false` gesetzt
* [!DNL Visual Experience Composer] Vorschläge mit `renderAttempted` Markierung `false`
* [!DNL Visual Experience Composer] Vorschläge für eine Einzelseiten-Programmansicht mit `renderAttempted` Markierung `false`

#### Bei Ansicht - Änderung (für Ansichten im Cache):

* Auf Visual Experience Composer basierende Vorschläge für eine Einzelseiten-Programmansicht mit `renderAttempted` Markierung `false`

### Aktualisierung eines einzelnen Profils

Mit dem [!DNL Web SDK] können Sie das Profil zum [!DNL Target] Profil und zum [!DNL Web SDK] als Erlebnisereignis aktualisieren.

Um ein [!DNL Target] zu aktualisieren, stellen Sie sicher, dass die Profildaten mit den folgenden Informationen übergeben werden:

* Unter `"data {"`
* Unter `"__adobe.target"`
* `"profile."`

| Schlüssel | Typ | Beschreibung |
| --- | --- | --- |
| `renderDecisions` | Boolesch | Weist die Personalisierungskomponente an, ob DOM-Aktionen interpretiert werden sollen |
| `decisionScopes` | `<String>` | Eine Liste der Bereiche, für die Entscheidungen abgerufen werden sollen |
| `xdm` | Objekt | In XDM formatierte Daten, die als Erlebnisereignis in Web SDK landen |
| `data` | Objekt | Beliebige Schlüssel/Wert-Paare, die an [!DNL Target] Lösungen unter der Zielklasse gesendet werden. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Speichern von Profil- oder Entitätsparametern verzögern, bis dem Endbenutzer Inhalte angezeigt wurden**

Um Aufzeichnungsattribute im Profil zu verzögern, bis der Inhalt angezeigt wurde, legen Sie in Ihrer Anfrage `data.adobe.target._save=false` fest.

Beispielsweise enthält Ihre Website drei Entscheidungsumfänge, die drei Kategorienlinks auf der Website entsprechen (Männer, Frauen und Kinder), und Sie möchten die Kategorie verfolgen, die der Benutzer letztendlich besucht hat. Senden Sie diese Anfragen, wobei das `__save`-Flag auf `false` gesetzt ist, um zu vermeiden, dass die Kategorie zum Zeitpunkt der Inhaltsanforderung beibehalten wird. Nachdem der Inhalt visualisiert wurde, senden Sie die richtige Payload (einschließlich `eventToken` und `stateToken`), damit die entsprechenden Attribute aufgezeichnet werden.

Im folgenden Beispiel wird eine Nachricht im Stil von trackEvent gesendet, Profilskripte ausgeführt, Attribute gespeichert und das Ereignis sofort aufgezeichnet.

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
        "__adobe": {
            "target": {
                " __save": true|false,
                //defaults to true if omitted
                "profile.gender": "female",
                "profile.age": 30,
                "entity.name": "T-shirt",
                "entity.id": "1234"
            }
        }
    }
})
```

>[!NOTE]
>
>Wenn die `__save`-Anweisung ausgelassen wird, erfolgt das Speichern der Profil- und Entitätsattribute sofort. Die `__save`-Direktive ist nur für Profilattribute und Entitätsdetails relevant.

## Empfehlungen anfordern

In der folgenden Tabelle sind [!DNL Recommendations] Attribute aufgeführt und es wird angegeben, ob sie über die [!DNL Web SDK] unterstützt werden:

| Kategorie | Attribut | Support-Status |
| --- | --- | --- |
| Recommendations - Standardattribute von Entitäten | entity.id | „Unterstützt“ |
|  | entity.name | „Unterstützt“ |
|  | entity.categoryId | „Unterstützt“ |
|  | entity.pageUrl | „Unterstützt“ |
|  | entity.thumbnailUrl | „Unterstützt“ |
|  | entity.message | „Unterstützt“ |
|  | entity.value | „Unterstützt“ |
|  | entity.inventory | „Unterstützt“ |
|  | entity.brand | „Unterstützt“ |
|  | entity.margin | „Unterstützt“ |
|  | entity.event.detailsOnly | „Unterstützt“ |
| Recommendations - Benutzerdefinierte Entitätsattribute | entity.yourCustomAttributeName | „Unterstützt“ |
| Recommendations - Reservierte mBox-/Seitenparameter | excludedIds | „Unterstützt“ |
|  | cartIds | „Unterstützt“ |
|  | productPurchasedId | „Unterstützt“ |
| Seite oder Elementkategorie für Kategorieaffinität | user.categoryId | „Unterstützt“ |

**Senden von Recommendations-Attributen an [!DNL Target]:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Mbox-Konversionsmetriken anzeigen {#display-mbox-conversion-metrics}

Das folgende Beispiel zeigt, wie Sie Mbox-Konversionen für die Anzeige verfolgen und Profilparameter an [!DNL Target] senden können, ohne sich für Inhalte oder Aktivitäten qualifizieren zu müssen.

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| Eigenschaft | Beschreibung |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | Der Umfang, mit dem die Erfolgsmetrik verknüpft werden soll (wodurch sie einer bestimmten Aktivität auf der Target-Seite zugeordnet wird). |
| `xdm._experience.decisioning.propositions[x].eventType` | Eine Zeichenfolge, die den beabsichtigten Ereignistyp beschreibt. Legen Sie dies für diesen Anwendungsfall auf `"decisioning.propositionDisplay"` fest. |

## Debugging

mboxTrace und mboxDebug werden nicht mehr unterstützt. Verwenden Sie stattdessen eine Methode vom [Web SDK-Debugging](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/use-cases/debugging).

## Terminologie  

**Vorschläge**: In [!DNL Target] korrelieren Vorschläge mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

**Schema**: Das Schema einer Entscheidung ist der Typ des Angebots in [!DNL Target].

**Umfang**: Der Umfang der Entscheidung. In [!DNL Target] ist der Umfang die Mbox. Die globale Mbox ist der `__view__`.

**XDM**: Das XDM wird in Punktnotation serialisiert und dann als Mbox-Parameter in [!DNL Target] eingefügt.
