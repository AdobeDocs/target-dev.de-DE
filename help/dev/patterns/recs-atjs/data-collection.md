---
title: Konfigurieren der Datenerfassung
description: Stellen Sie sicher, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
TQID: https://experienceleague.adobe.com/fg3xJnwYAVyz-N-xzT5Piu35Ajd2UMEvuTvTQs2wj3c
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 401
ht-degree: 1%

---

# Konfigurieren der Datenerfassung

Befolgen Sie die Schritte im *Datenerfassung*-Diagramm, um sicherzustellen, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie im Vollbildmodus anzuzeigen.

Die Datenschicht ist beim Laden der Seite bereit oder die Datenschicht ändert sich nach dem Laden der Seite.

Wenn Sie bereits während der Initialisierungsphase von [&#x200B; Daten zugeordnet haben](/help/dev/patterns/recs-atjs/initialize-sdk.md) müssen Sie die Schritte in diesem Diagramm ausführen, wenn:

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

+++Details anzeigen

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

+++Details anzeigen

**Messwerte**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=de){target=_blank}

**Zu beachten**

* Eine alternative Möglichkeit, Entitätsattribute zu übergeben, besteht darin, den Produktkatalog in der [!DNL Target]-Benutzeroberfläche zu aktualisieren, um [Recommendations-Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=de){target=_blank} zu verwenden.
* Die Übergabe von Entitätsattributen ist nur auf Seiten anwendbar, auf denen Produktkatalogdaten in der Datenschicht verfügbar sind.
* Die Übergabe des `entity.event.detailsOnly=true` bei jedem Aufruf hat Priorität.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.3 Auslösen der Adobe Target Track-API {#fire-api}

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, auch gesendet werden.

+++Details anzeigen

![Diagramm zur Fire Adobe Target Track-API](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit der Funktion [targetPageParams“ durchgeführt &#x200B;](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Messwerte**

* [adobe.target.trackEvent()-Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Aktionen**

Verwenden Sie [adobe.target.trackEvent()-Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) um alle Daten zu senden, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 3: [Rendern von Erlebnissen](/help/dev/patterns/recs-atjs/render-experiences.md) fort
