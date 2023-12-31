---
title: Erlebnisse rendern
description: Stellen Sie sicher, dass alle erforderlichen Schritte zum Rendern von Erlebnissen in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
source-git-commit: 723bb2f33a011995757009193ee9c48757ae1213
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 7%

---

# Erlebnisse rendern

Führen Sie die Schritte im Abschnitt *Render-Erlebnisse* -Diagramm, um sicherzustellen, dass alle erforderlichen Aufgaben zum Rendern von Erlebnissen in der richtigen Reihenfolge ausgeführt werden.

>[!NOTE]
>
>Wenn Sie die automatische Seitenladeanforderung während der [Schritt &quot;Automatische Seitenladeanforderung konfigurieren&quot;](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) in *SDKS initialisieren* können Sie diese Aktivität überspringen, es sei denn, Sie möchten das Adobe Target SDK aufrufen, um zusätzliche Erlebnisse mithilfe einer regionalen Ortsanforderung zu rendern.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

## Diagramm für Rendering-Erlebnisse {#diagram}

Die automatische standardmäßige Flackerbehandlung mit at.js ist nur dann sinnvoll, wenn Sie [!UICONTROL Automatische Seitenladeanforderung] aktiviert. Diese Option blendet den gesamten HTML-Textkörper aus, während die Erlebnisse abgerufen werden [!DNL Target]. In diesem Fall ist es Ihre Verantwortung, mit Flackern umzugehen. Suchen Sie nach Implementierungsmustern, die für die Flackerverarbeitung verfügbar sind, um Hinweise zu erhalten.

>[!NOTE]
>
>Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten. Die Schrittzahlen sind nicht in einer bestimmten Reihenfolge und spiegeln nicht die Reihenfolge der Schritte wider, die in der [!DNL Target] Benutzeroberfläche beim Erstellen der Aktivität.

![Diagramm für Rendering-Erlebnisse](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [3.1. Promotion](#promotion)
* [3.2: Warenkorbbasierte Kriterien](#cart)
* [3.3: Beliebtheitsbasierte Kriterien](#popularity)
* [3.4: Artikelbasierte Kriterien](#item)
* [3.5: Benutzerbasierte Kriterien](#user)
* [3.6: Benutzerdefinierte Kriterien](#custom)
* [3.7: Geben Sie in Einschlussregeln verwendete Attribute an](#inclusion)
* [3.8: Ausgeschlossene IDs bereitstellen](#exclude)
* [3.9: Stellen Sie Entitätsattribute bereit, um den Produktkatalog für Recommendations zu aktualisieren](#entity-attributes)
* [3.10: Geben Sie als Schlüssel für Einschlussregeln verwendete Profilattribute an](#keys)
* [3.11: Seitenladeanforderung auslösen](#fire)
* [3.12: Anforderung eines regionalen Standorts auslösen](#location)

## 3.1. Promotion {#promotion}

Fügen Sie Promotionsartikel hinzu und steuern Sie deren Platzierung in Ihrem Empfehlungsentwurf, indem Sie im [!DNL Target] Benutzeroberfläche beim Erstellen der Aktivität.

+++Siehe Details

**Verfügbare Optionen**

* Hervorheben nach IDs
* [Hervorheben nach Sammlung](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Hervorheben nach Attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entitätsparameter erforderlich**

* Elementattribute in Promotions müssen bei Verwendung der Option &quot;Bewerben nach Attribut&quot;übergeben werden.

**Lesungen**

* [Hinzufügen von Promotions](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.2: Warenkorbbasierte Kriterien {#cart}

Machen Sie Empfehlungen basierend auf den Inhalten des Warenkorbs des Benutzers.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Personen, die diese ansahen, sahen diese an]
* [!UICONTROL Personen, die diese ansahen, kauften diese]
* [!UICONTROL Personen, die diese kauften, kauften diese]

**Entitätsparameter erforderlich**

* cartIds

**Lesungen**

* [Warenkorbbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.3: Beliebtheitsbasierte Kriterien {#popularity}

Machen Sie Empfehlungen basierend auf der allgemeinen Beliebtheit eines Artikels auf Ihrer Site oder auf der Beliebtheit von Artikeln in der bevorzugten oder am häufigsten angezeigten Kategorie, Marke, Genre usw. eines Besuchers.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Am häufigsten angezeigt auf der gesamten Site]
* [!UICONTROL Am häufigsten angezeigt nach Kategorie]
* [!UICONTROL Am häufigsten nach Elementattribut angezeigt]
* [!UICONTROL Topverkäufe auf der gesamten Site]
* [!UICONTROL Topverkäufe nach Kategorie]
* [!UICONTROL Topverkäufe nach Elementattribut]
* [!UICONTROL Top nach Analytics-Metrik]

**Entitätsparameter erforderlich**

* `entity.categoryId` oder das Elementattribut für die Beliebtheit, wenn das Kriterium auf dem aktuellen Attribut oder dem Elementattribut basiert.
* Für die am häufigsten angezeigten/am häufigsten verkauften Artikel auf der Site muss nichts übergeben werden.

**Lesungen**

* [Popularitätsbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.4: Artikelbasierte Kriterien {#item}

Empfehlungen aussprechen, die darauf basieren, ähnliche Artikel wie ein Artikel zu finden, den der Benutzer anzeigt oder kürzlich angesehen hat.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Personen, die das ansahen, sahen auch dies an]
* [!UICONTROL Personen, die das ansahen, kauften dies]
* [!UICONTROL Personen, die das kauften, kauften dies]
* [!UICONTROL Elemente mit ähnlichen Attributen]

**Entitätsparameter erforderlich**

* `entity.id`
* Wenn ein Profilattribut als Schlüssel verwendet wird

**Lesungen**

* [Artikelbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.5: Benutzerbasierte Kriterien {#user}

Empfehlungen basierend auf dem Benutzerverhalten erstellen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Vor Kurzem aufgerufene Artikel ]
* [!UICONTROL Empfohlen für Sie]

**Entitätsparameter erforderlich**

* `entity.id`

**Lesungen**

* [Benutzerbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.6: Benutzerdefinierte Kriterien {#custom}

Machen Sie Empfehlungen basierend auf einer benutzerdefinierten Datei, die Sie hochladen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Benutzerspezifischer Algorithmus]

**Entitätsparameter erforderlich**

`entity.id` oder das Attribut, das als Schlüssel für den benutzerspezifischen Algorithmus verwendet wird

**Lesungen**

* [Benutzerdefinierte Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.7: Geben Sie in Einschlussregeln verwendete Attribute an {#inclusion}

+++Siehe Details

**Lesungen**

* [Verwenden dynamischer und statischer Einschlussregeln](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.8: Ausgeschlossene IDs bereitstellen {#exclude}

Übergeben Sie Entitäts-IDs für Entitäten, die Sie aus Ihren Empfehlungen ausschließen möchten. Beispielsweise können Sie Artikel ausschließen, die sich bereits im Warenkorb befinden.

+++Siehe Details

**Lesungen**

* [Kann ich eine Entität dynamisch ausschließen?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.9: Stellen Sie Entitätsattribute bereit, um den Produktkatalog für [!DNL Recommendations] {#entity-attributes}

+++Siehe Details

**Lesungen**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Sie können diesen Schritt auch durch Erstellen von [Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} mithilfe der [!DNL Target] Benutzeroberfläche zum Aktualisieren des Produktkatalogs für [!DNL Recommendations].

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.10: Geben Sie als Schlüssel für Einschlussregeln verwendete Profilattribute an {#keys}

Geben Sie die Profilattribute an, die als Schlüssel für Einschlussregeln in den oben genannten Recommendations-Kriterien verwendet werden.

+++ Siehe Details

**Lesungen**

* [Profilattribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.11: Seitenladeanforderung auslösen {#fire}

Dieser Schritt Trigger eine [!DNL Delivery API] Aufruf mit `execute` > `pageLoad` Nutzlast in der Anfrage. Die `getOffers()` -Methode ruft das Erlebnis ab und `applyOffers()` rendert das Erlebnis auf der Seite. Die `pageLoad` -Anfrage ist zum Rendern von Erlebnissen erforderlich, die in der [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++Siehe Details

![Anforderungsdiagramm für Seitenladeanforderungen auslösen](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit dem `targetPageParams` -Funktion.

**Lesungen**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Aktionen**

* Verwenden Sie die `getOffers` und `applyOffers` -Methoden, um das Erlebnis mithilfe eines API-Aufrufs für Seitenladeanfragen abzurufen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.12: Regionale Standortanforderung auslösen (#location)

Dieser Schritt Trigger eine [!DNL Delivery API] Aufruf mit `execute` > `mboxes` Nutzlast in der Anfrage. Die `getOffers` -Methode ruft das Erlebnis ab und `applyOffers` rendert das Erlebnis auf der Seite. Sie können mehr als eine Mbox unter der `execute` > `mboxes` Nutzlast.

+++Siehe Details

![Diagramm für regionale Standortanforderung auslösen](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit dem `targetPageParams` -Funktion.

**Lesungen**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Aktionen**

* Verwenden Sie die `getOffers` und `applyOffers` -Methoden, um das Erlebnis mithilfe eines API-Aufrufs für Seitenladeanfragen abzurufen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 4 fort: [Target benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md).