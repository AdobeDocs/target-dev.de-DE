---
title: Datenerfassung konfigurieren
description: Stellen Sie sicher, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: c6d779f14a53193ff423678ebe96fdaacc57be5d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---

# Datenerfassung konfigurieren

Führen Sie die Schritte im Abschnitt *Datenerfassung* -Diagramm, um sicherzustellen, dass alle für die Datenerfassung erforderlichen Aufgaben in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

Die Datenschicht ist beim Laden der Seite bereit oder die Datenschicht ändert sich nach dem Laden der Seite.

Wenn Sie bereits Daten während der [SDK-Phase initialisieren](/help/dev/patterns/recs-atjs/initialize-sdk.md)müssen Sie die Schritte in diesem Diagramm ausführen, wenn:

* Ihre Datenschicht wird auf beliebige Weise auf derselben Seite erweitert und Sie möchten diese zusätzlichen Daten an senden [!DNL Target]
* Sie möchten Produktkatalogdaten an senden [!DNL Target Recommendations]

## Datendiagramm abrufen {#diagram}

Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten.

![Datenerfassungsdiagramm](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [2.1: Konfigurieren der Datenzuordnung](#configure)
* [2.2 Verknüpfung zu Entitätsattributen](#entity-attributes)
* [2.3 Adobe Target Track-API auslösen](#fire-api)

## 2.1: Konfigurieren der Datenzuordnung {#configure}

Dieser Schritt stellt sicher, dass alle Daten, an die gesendet werden müssen, [!DNL Adobe Target] festgelegt ist.

+++Siehe Details

![Diagramm für die Datenzuordnung konfigurieren](/help/dev/patterns/recs-atjs/assets/cofigure-data-mapping.png){width="300" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte alle Daten enthalten, die an gesendet werden müssen. [!DNL Target].

**Lesungen**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die `targetPageParams()` -Funktion zum Festlegen aller erforderlichen Daten, die an gesendet werden müssen [!DNL Target].

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.2: Link zu Entitätsattributen {#entity-attributes}

Link zu Entitätsattributen zur Aktualisierung des Produktkatalogs für [!DNL Target Recommendations].

+++Siehe Details

**Lesungen**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Zu beachten**

* Eine alternative Methode zur Weitergabe von Entitätsattributen besteht darin, den Produktkatalog im [!DNL Target] Zu verwendende Benutzeroberfläche [Recommendations-Produkt-Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* Die Übergabe von Entitätsattributen ist nur auf Seiten möglich, auf denen Produktkatalogdaten in der Datenschicht verfügbar sind.
* Übergeben der `entity.event.detailsOnly=true` -Parameter in jedem -Aufruf hat Priorität.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 2.3 Adobe Target Track-API auslösen {#fire-api}

Dieser Schritt stellt sicher, dass alle Daten, an die gesendet werden müssen, [!DNL Target] gesendet.

+++Siehe Details

![Adobe Target Track-API-Diagramm auslösen](/help/dev/patterns/recs-atjs/assets/fire-track-api.png){width="300" zoomable="yes"}

**Voraussetzungen**

* Die gesamte Datenzuordnung muss mit dem [targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lesungen**

* [adobe.target.trackEvent() -Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**Aktionen**

Verwendung [adobe.target.trackEvent() -Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) , um alle Daten zu senden, die an [!DNL Target].

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)
