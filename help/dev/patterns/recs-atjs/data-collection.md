---
title: Datenerfassung konfigurieren
description: Stellen Sie sicher, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Datenerfassung konfigurieren

Führen Sie die Schritte im Diagramm *Datenerfassung* aus, um sicherzustellen, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

Die Datenschicht ist beim Laden der Seite bereit oder die Datenschicht ändert sich nach dem Laden der Seite.

Wenn Sie während der [Initialize SDK-Phase](/help/dev/patterns/recs-atjs/initialize-sdk.md) bereits Daten zugeordnet haben, müssen Sie die Schritte in diesem Diagramm ausführen, wenn:

* Ihre Datenschicht wird auf beliebige Weise auf derselben Seite erweitert und Sie möchten diese zusätzlichen Daten an [!DNL Target] senden
* Sie möchten Produktkatalogdaten an [!DNL Target Recommendations] senden.

## Datendiagramm abrufen {#diagram}

Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten.

![Datenerfassungsdiagramm](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [2.1: Konfigurieren der Datenzuordnung](#configure)
* [2.2 Verknüpfung zu Entitätsattributen](#entity-attributes)
* [2.3 Adobe Target Track-API auslösen](#fire-api)

## 2.1: Konfigurieren der Datenzuordnung {#configure}

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Adobe Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Diagramm zur Datenzuordnung konfigurieren](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten fertig sein, die an [!DNL Target] gesendet werden müssen.

**Lesungen**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.2: Link zu Entitätsattributen {#entity-attributes}

Link zu Entitätsattributen zur Aktualisierung des Produktkatalogs für [!DNL Target Recommendations].

+++Siehe Details

**Lesungen**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Zu beachten**

* Eine alternative Methode zur Übergabe von Entitätsattributen besteht darin, den Produktkatalog in der Benutzeroberfläche von [!DNL Target] zu aktualisieren, um [Recommendations-Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} zu verwenden.
* Die Übergabe von Entitätsattributen ist nur auf Seiten möglich, auf denen Produktkatalogdaten in der Datenschicht verfügbar sind.
* Die Übergabe des Parameters `entity.event.detailsOnly=true` bei jedem Aufruf hat Priorität.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.3 Adobe Target Track-API auslösen {#fire-api}

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, gesendet werden.

+++Siehe Details

![Adobe Target Tracking-API-Diagramm auslösen](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit der Funktion [targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) durchgeführt worden sein.

**Lesungen**

* [adobe.target.trackEvent() -Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Aktionen**

Verwenden Sie [adobe.target.trackEvent() method](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) , um alle Daten zu senden, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 3 fort: [Erlebnisse rendern](/help/dev/patterns/recs-atjs/render-experiences.md)
