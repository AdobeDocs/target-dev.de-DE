---
title: Rendern von Erlebnissen
description: Stellen Sie sicher, dass alle erforderlichen Schritte zum Rendern von Erlebnissen in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---

# Rendern von Erlebnissen

Befolgen Sie die Schritte im Diagramm *Erlebnisse rendern*, um sicherzustellen, dass alle erforderlichen Aufgaben zum Rendern von Erlebnissen in der richtigen Reihenfolge ausgeführt werden.

>[!NOTE]
>
>Wenn Sie die automatische Seitenladeanfrage während des Schritts [Konfigurieren einer automatischen Seitenladeanfrage](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) in *SDKS initialisieren* aktiviert haben, können Sie diese Aktivität überspringen, es sei denn, Sie möchten den Adobe Target-SDK aufrufen, um zusätzliche Erlebnisse mithilfe einer regionalen Standortanfrage zu rendern.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie im Vollbildmodus anzuzeigen.

## Rendering-Erlebnisdiagramm {#diagram}

Eine automatische vordefinierte Flackerbehandlung, die mit at.js verfügbar ist, ist nur sinnvoll, wenn Sie [!UICONTROL Automatic Page Load Request] aktiviert haben. Diese Option blendet den gesamten HTML-Textkörper aus, während die Erlebnisse aus [!DNL Target] abgerufen werden. In diesem Fall liegt es in Ihrer Verantwortung, mit Flackern umzugehen. Suchen Sie nach verfügbaren Implementierungsmustern für die Flimmerhandhabung, um eine Anleitung zu erhalten.

>[!NOTE]
>
>Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten. Die Schrittnummern befinden sich in keiner bestimmten Reihenfolge und entsprechen nicht der Reihenfolge der Schritte, die in der [!DNL Target]-Benutzeroberfläche beim Erstellen der Aktivität ausgeführt wurden.

![Rendering-Erlebnisdiagramm](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [3.1: Absatzförderung](#promotion)
* [3.2: Warenkorb-basierte Kriterien](#cart)
* [3.3: Beliebtheitskriterien](#popularity)
* [3.4: Kriterien auf der Grundlage von Artikeln](#item)
* [3.5: Benutzerbasierte Kriterien](#user)
* [3.6: Benutzerdefinierte Kriterien](#custom)
* [3.7: Angabe der in Einschlussregeln verwendeten Attribute](#inclusion)
* [3.8: Angabe der excludedIds](#exclude)
* [3.9: Entitätsattribute angeben, um den Produktkatalog für Recommendations zu aktualisieren](#entity-attributes)
* [3.10: Geben Sie Profilattribute an, die als Schlüssel für Einschlussregeln verwendet werden](#keys)
* [3.11: Auslösen einer Seitenladeanforderung](#fire)
* [3.12: Feuer Regionale Standortanfrage](#location)

## 3.1: Absatzförderung {#promotion}

Fügen Sie hochgestufte Elemente hinzu und steuern Sie deren Platzierung im Recommendations-Design, indem Sie in der [!DNL Target]-Benutzeroberfläche beim Erstellen der Aktivität Heraufstufungen nach vorne oder hinten auswählen.

+++Siehe Details

**Verfügbare Optionen**

* Nach IDs hochstufen
* [Nach Sammlung bewerben](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Hochstufen nach Attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entitätsparameter erforderlich**

* Elementattribute in Promotions müssen bei Verwendung der Option „Nach Attribut bewerben“ übergeben werden.

**Messwerte**

* [Hinzufügen von Promotions](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.2: Warenkorb-basierte Kriterien {#cart}

Empfehlungen auf der Grundlage des Warenkorbinhalts des Benutzers aussprechen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Entitätsparameter erforderlich**

* cartIds

**Messwerte**

* [Warenkorbbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.3: Beliebtheitskriterien {#popularity}

Empfehlungen auf der Grundlage der allgemeinen Popularität eines Elements auf Ihrer Website oder auf der Grundlage der Popularität von Elementen innerhalb der Lieblings- oder am häufigsten angezeigten Kategorie, Marke, Genre usw. eines Besuchers.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Entitätsparameter erforderlich**

* `entity.categoryId` oder das Elementattribut für Popularität basierend auf , wenn das Kriterium auf dem aktuellen oder dem Elementattribut basiert.
* Nichts darf für Am häufigsten angezeigt/Am häufigsten verkauft über die Website weitergegeben werden.

**Messwerte**

* [Beliebtheitsbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.4: Kriterien auf der Grundlage von Artikeln {#item}

Empfehlungen aussprechen, die darauf basieren, ähnliche Elemente zu finden wie ein Element, das der Benutzer gerade anzeigt oder kürzlich angeschaut hat.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Entitätsparameter erforderlich**

* `entity.id`
* Wenn ein Profilattribut als Schlüssel verwendet wird

**Messwerte**

* [Elementbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.5: Benutzerbasierte Kriterien {#user}

Empfehlungen auf der Grundlage des Benutzerverhaltens aussprechen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Entitätsparameter erforderlich**

* `entity.id`

**Messwerte**

* [Benutzerbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.6: Benutzerdefinierte Kriterien {#custom}

Empfehlungen basierend auf einer benutzerdefinierten Datei geben, die Sie hochladen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Custom algorithm]

**Entitätsparameter erforderlich**

`entity.id` oder das als Schlüssel für den benutzerdefinierten Algorithmus verwendete Attribut

**Messwerte**

* [Benutzerdefinierte Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.7: Angabe der in Einschlussregeln verwendeten Attribute {#inclusion}

+++Siehe Details

**Messwerte**

* [Verwenden dynamischer und statischer Einschlussregeln](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.8: Angabe der excludedIds {#exclude}

Übergeben Sie Entitäts-IDs für Entitäten, die Sie aus Ihren Empfehlungen ausschließen möchten. Beispielsweise können Sie Artikel ausschließen, die sich bereits im Warenkorb befinden.

+++Siehe Details

**Messwerte**

* [Kann ich eine Entität dynamisch ausschließen?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.9: Entitätsattribute angeben, um den Produktkatalog für [!DNL Recommendations] zu aktualisieren {#entity-attributes}

+++Siehe Details

**Messwerte**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

Sie können diesen Schritt auch durchführen, indem Sie [Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} über die [!DNL Target]-Benutzeroberfläche erstellen, um den Produktkatalog für [!DNL Recommendations] zu aktualisieren.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.10: Geben Sie Profilattribute an, die als Schlüssel für Einschlussregeln verwendet werden {#keys}

Geben Sie die Profilattribute an, die als Schlüssel für Einschlussregeln in den oben genannten Recommendations-Kriterien verwendet werden.

+++ Details anzeigen

**Messwerte**

* [Profilattribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.11: Auslösen einer Seitenladeanforderung {#fire}

In diesem Schritt wird ein [!DNL Delivery API]-Aufruf mit `execute` > Payload `pageLoad` in der Anfrage Trigger. Die `getOffers()`-Methode ruft das Erlebnis ab und rendert das Erlebnis `applyOffers()` auf der Seite. Die `pageLoad`-Anfrage wird für das Rendern von Erlebnissen benötigt, die in [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) verfasst wurden.

+++Siehe Details

![Diagramm „Auslösen einer Seitenladeanfrage](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Alle Datenzuordnungen müssen mit der `targetPageParams`-Funktion vorgenommen werden.

**Messwerte**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Aktionen**

* Verwenden Sie die `getOffers` und `applyOffers` Methoden, um das Erlebnis mithilfe eines Seitenladeanfrage-API-Aufrufs abzurufen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 3.12: Feuer Regionale Standortanfrage (#location)

In diesem Schritt wird ein [!DNL Delivery API]-Aufruf mit `execute` > Payload `mboxes` in der Anfrage Trigger. Die `getOffers`-Methode ruft das Erlebnis ab und rendert das Erlebnis `applyOffers` auf der Seite. Sie können unter `execute` > `mboxes` Payload mehr als eine Mbox senden.

+++Siehe Details

![Diagramm mit regionalen Standortanfragen auslösen](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Alle Datenzuordnungen müssen mit der `targetPageParams`-Funktion vorgenommen werden.

**Messwerte**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**Aktionen**

* Verwenden Sie die `getOffers` und `applyOffers` Methoden, um das Erlebnis mithilfe eines Seitenladeanfrage-API-Aufrufs abzurufen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 4: [Target benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md) fort.
