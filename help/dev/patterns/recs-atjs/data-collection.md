---
title: Konfigurieren der Datenerfassung
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

# Konfigurieren der Datenerfassung

Befolgen Sie die Schritte im *Datenerfassung*-Diagramm, um sicherzustellen, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie im Vollbildmodus anzuzeigen.

Die Datenschicht ist beim Laden der Seite bereit oder die Datenschicht ändert sich nach dem Laden der Seite.

SDK Wenn Sie bereits während der Initialisierungsphase von [ Daten zugeordnet haben](/help/dev/patterns/recs-atjs/initialize-sdk.md) müssen Sie die Schritte in diesem Diagramm ausführen, wenn:

* Ihre Datenschicht wird auf dieselbe Seite in beliebiger Weise erweitert, und Sie möchten diese zusätzlichen Daten an [!DNL Target] senden
* Sie möchten Produktkatalogdaten an [!DNL Target Recommendations] senden

## Datendiagramm erfassen {#diagram}

Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten.

![Datenerfassungsdiagramm](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [2.1: Konfigurieren der Datenzuordnung](#configure)
* [2.2 Relation zu Entitätsattributen](#entity-attributes)
* [2.3 Auslösen der Adobe Target Track-API](#fire-api)

## 2.1: Konfigurieren der Datenzuordnung {#configure}

Mit diesem Schritt stellen Sie sicher, dass alle Daten, die an [!DNL Adobe Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Konfigurieren des Datenzuordnungsdiagramms](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten bereit sein, die an [!DNL Target] gesendet werden müssen.

**Messwerte**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.2: Relation zu Entitätsattributen {#entity-attributes}

Link zu Entitätsattributen, um den Produktkatalog für [!DNL Target Recommendations] zu aktualisieren.

+++Siehe Details

**Messwerte**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Zu beachten**

* Eine alternative Möglichkeit, Entitätsattribute zu übergeben, besteht darin, den Produktkatalog in der [!DNL Target]-Benutzeroberfläche zu aktualisieren, um [Recommendations-Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank} zu verwenden.
* Die Übergabe von Entitätsattributen ist nur auf Seiten anwendbar, auf denen Produktkatalogdaten in der Datenschicht verfügbar sind.
* Die Übergabe des `entity.event.detailsOnly=true` bei jedem Aufruf hat Priorität.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.3 Auslösen der Adobe Target Track-API {#fire-api}

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, auch gesendet werden.

+++Siehe Details

![Diagramm zur Fire Adobe Target Track-API](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit der Funktion [targetPageParams“ durchgeführt ](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Messwerte**

* [adobe.target.trackEvent()-Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Aktionen**

Verwenden Sie [adobe.target.trackEvent()-Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) um alle Daten zu senden, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 3: [Rendern von Erlebnissen](/help/dev/patterns/recs-atjs/render-experiences.md) fort
