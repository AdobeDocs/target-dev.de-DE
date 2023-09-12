---
title: Initialisieren von SDKs
description: Stellen Sie sicher, dass alle erforderlichen Schritte zum Laden der [!DNL Adobe Target] Die JavaScript-Bibliothek at.js wird in der richtigen Reihenfolge ausgeführt.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 6cd78f8e3cbdd97a09b0cb6ca3af55994e85f819
workflow-type: tm+mt
source-wordcount: '1791'
ht-degree: 8%

---

# Initialisieren von SDKs

Führen Sie die Schritte im Abschnitt *SDK initialisieren* Diagramm, um sicherzustellen, dass alle erforderlichen Aufgaben zum Laden der [!DNL Adobe Target] Die JavaScript-Bibliothek at.js wird in der richtigen Reihenfolge ausgeführt.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

## SDK-Diagramm initialisieren {#diagram}

Bei mehrseitigen Anwendungen erfolgt dieser Fluss jedes Mal, wenn die Seite neu geladen wird, oder der Besucher zu einer neuen Seite auf der Website navigiert.

Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten.

![SDK-Diagramm initialisieren](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [1.1: Laden des Besucher-API-SDK](#load)
* [1.2: Festlegen der Kunden-ID](#set)
* [1.3: Automatische Seitenladeanforderung konfigurieren](#automatic)
* [1.4: Flackern-Handhabung konfigurieren](#flicker)
* [1.5: Konfigurieren der Datenzuordnung](#data-mapping)
* [1.6. Promotion](#promotion)
* [1.7: Warenkorbbasierte Kriterien](#cart)
* [1.8: Beliebtheitsbasierte Kriterien](#popularity)
* [1.9: Artikelbasierte Kriterien](#item)
* [1.10: Benutzerbasierte Kriterien](#user)
* [1.11: Benutzerdefinierte Kriterien](#custom)
* [1.12: Geben Sie in Einschlussregeln verwendete Attribute an](#inclusion)
* [1.13: Ausgeschlossene IDs angeben](#exclude)
* [1.14: Parameter entity.event.detailsOnly=true übergeben](#true)
* [1.15: Remote-Daten-Mapping konfigurieren](#remote)
* [1.16: at.js laden](#web)

## 1.1: Laden des Besucher-API-SDK {#load}

Dieser Schritt stellt sicher, dass `VisitorAPI.js` -Bibliothek korrekt geladen, konfiguriert und initialisiert wird.

+++Siehe Details

![Besucher-API-SDK-Diagramm laden](/help/dev/patterns/recs-atjs/assets/load-visitor-api-sdk.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Zur Verwendung des Besucher-ID-/API-Service muss Ihr Unternehmen für die [!DNL Adobe Experience Cloud] und verfügen über eine [!UICONTROL Organisations-ID]. Weitere Informationen finden Sie unter [Experience Cloud-Voraussetzungen: Organisations-ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} im *Hilfe zu Identity Service* Handbuch.
* Sie benötigen die `VisitorAPI.js` -Datei. Sie sollten diese Datei bereits haben, wenn Sie [!DNL Adobe Analytics] implementiert. Diese Datei kann auch über die [[!DNL Adobe Experience Platform] Tag-Erweiterung](https://experienceleague.adobe.com/docs/tags.html){target=_blank} or can be downloaded from the [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**VisitorAPI.js konfigurieren und referenzieren**

Weitere Informationen finden Sie unter [Implementieren des Experience Cloud-Diensts für Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Lesungen**

* [Übersicht über den Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Über den ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies und der Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Anfordern und Festlegen von IDs durch den Experience Cloud Identity-Dienst](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Grundlegendes zu ID-Synchronisierung und Übereinstimmungsraten](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Aktionen**

* Einbetten der `VisitorAPI.js` -Datei auf Ihren Webseiten.
* Lesen Sie über [verfügbare Konfigurationen für den Besucher-ID-/API-Dienst](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Nach dem `VisitorAPI.js` -Datei geladen ist, verwenden Sie die `Visitor.getInstance` -Methode, um mit den benötigten Konfigurationen zu initialisieren.
* Machen Sie sich mit dem [verfügbare Methoden](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.2: Festlegen der Kunden-ID {#set}

Dieser Schritt stellt sicher, dass die bekannten IDs (CRM-ID, Benutzer-ID usw.) Ihrer Besucher mit der anonymen ID von [!DNL Adobe] für geräteübergreifende Personalisierung.

+++Siehe Details

![Kunden-ID festlegen](/help/dev/patterns/recs-atjs/assets/set-customer-id.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die bekannte ID der Besucher sollte auf der Datenschicht verfügbar sein.

**Kunden-ID festlegen**
Weitere Informationen finden Sie unter [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Lesungen**

* [Echtzeit-Profilsynchronisation für mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Aktionen**

* Verwendung `visitor.setCustomerIDs` , um die bekannte ID des Besuchers festzulegen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.3: Automatische Seitenladeanforderung konfigurieren {#automatic}

Dieser Schritt ermöglicht es at.js, alle Erlebnisse abzurufen, die beim Laden der JavaScript-Bibliotheksdatei at.js auf der Seite gerendert werden müssen.

+++Siehe Details

![Automatische Seitenladeanforderung konfigurieren](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Nicht alle Daten in der Datenschicht müssen an [!DNL Target]. Wenden Sie sich an Ihr Business-Team (Digital Marketing Team), um zu ermitteln, welche Daten für Experimente, Optimierung und Personalisierung nützlich sind. Nur diese Daten sollten an [!DNL Target].
* Stellen Sie sicher, dass Sie keine personenbezogenen Daten (PII) an senden [!DNL Target].

**Automatische Seitenladeanforderung konfigurieren**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lesungen**

Informationen zum `pageLoadEnabled` Einstellung in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie die `window.targetGlobalSettings` -Objekt, um automatische Seitenladeanfragen zu aktivieren.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.4: Flackern-Handhabung konfigurieren {#flicker}

Dieser Schritt stellt sicher, dass bei der Bereitstellung von Erlebnissen kein Seitenflackern auftritt.

+++Siehe Details

![Flackern-Handling-Diagramm konfigurieren](/help/dev/patterns/recs-atjs/assets/flicker-handling.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Erfahren Sie mehr mit dem für die Webseitenleistung zuständigen Team über die Vor- und Nachteile der Flackerverhinderung mithilfe der von at.js verwendeten Standardmethode. Sie können nach Designmustern suchen, mit denen Sie benutzerdefinierte Flacker-Handling-Lösungen wie Lader-Animation verwenden können. Wenn Sie kein Muster finden, können Sie ein neues Muster anfordern.

**Flackern konfigurieren**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Einstellung `bodyHidingEnabled` nach `true` blendet den gesamten Seitentext aus, während die Seitenladeanforderung ausgeführt wird. Wenn Sie die automatische Seitenladeanforderung aus irgendeinem Grund nicht aktiviert haben (z. B. Daten später nicht bereit), empfiehlt es sich, diese Einstellung auf `false`.

Wenn Sie `bodyHidingEnabled` Da Sie APLR nicht auslösen und die Seitenanforderung später auslösen möchten oder keine Flackerbehandlung benötigen, müssen Sie Ihre eigene Flackerbehandlung implementieren. Sie können das Flackern auf zwei Arten handhaben: das Ausblenden der zu prüfenden Abschnitte oder das Anzeigen einer Halbleiter für die zu testenden Abschnitte.

**Lesungen**

* [Verwaltung von Flackern mit „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Informationen zu den Objekten bodyHiddenStyle und bodyHidingEnabled in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie die `window.targetGlobalSettings` Objekt festlegen `bodyHiddenStyle` und `bodyHidingEnabled`.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.5: Konfigurieren der Datenzuordnung {#data-mapping}

Dieser Schritt stellt sicher, dass alle Daten, an die gesendet werden müssen, [!DNL Target] festgelegt ist.

+++Siehe Details

![Datenzuordnungsdiagramm](/help/dev/patterns/recs-atjs/assets/data-mapping.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte alle Daten enthalten, die an gesendet werden müssen [!DNL Target].
* Recommendations: Profil anreichern.
   * Pass `entity.id` zum Erfassen von Daten zu kürzlich angezeigten Kriterien und Elementen basierend auf Kriterien, die auf dem zuletzt angezeigten Produkt basieren.
   * Pass `entity.id` , um Daten für Beliebtheitskriterien basierend auf der Favoritenkategorie zu erfassen.
   * Übergeben Sie das Profilattribut, wenn benutzerdefinierte Kriterien darauf basieren oder in der Filterung von Einschlussregeln in beliebigen Kriterien verwendet werden.
* Recommendations: Erfassen Sie Produktdaten.
   * Andere (reservierte und benutzerdefinierte) Entitätsparameter können an die Erfassung oder Aktualisierung des Produktkatalogs in [!DNL Recommendations].
   * Der Produktkatalog kann auch mithilfe von Entitäts-Feeds mit dem [!DNL Target] Benutzeroberfläche oder API.

**Zuordnen von Daten zu[!DNL Target]**

Weitere Informationen finden Sie unter [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lesungen**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planen und Implementieren von Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Recommendations-Katalog einrichten](/help/dev/implement/recommendations/recommendations.md)

**Aktionen**

* Verwenden Sie die `targetPageParams()` -Funktion zum Festlegen aller erforderlichen Daten, die an gesendet werden müssen [!DNL Target].

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.6. Promotion {#promotion}

Fügen Sie Promotionsartikel hinzu und steuern Sie deren Platzierung in Ihren [!DNL Target Recommendations][-Designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Siehe Details

**Verfügbare Optionen**

* Hervorheben nach IDs
* [Hervorheben nach Sammlung](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Hervorheben nach Attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entitätsparameter erforderlich**

* Das Elementattribut in der Promotion muss bei Verwendung der Option &quot;Bewerben nach Attribut&quot;übergeben werden.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.7: Warenkorbbasierte Kriterien {#cart}

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

## 1.8: Beliebtheitsbasierte Kriterien {#popularity}

Machen Sie Empfehlungen basierend auf der allgemeinen Beliebtheit eines Artikels auf Ihrer Site oder auf der Beliebtheit von Artikeln in der bevorzugten oder am häufigsten angezeigten Kategorie, Marke, Genre usw. eines Benutzers.

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

* `entity.categoryId` oder das Elementattribut für die Beliebtheit, wenn das Kriterium auf dem aktuellen Element oder dem Elementattribut basiert.
* Für die am häufigsten angezeigten/am häufigsten verkauften Artikel auf der Site muss nichts übergeben werden.

**Lesungen**

* [Popularitätsbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.9: Artikelbasierte Kriterien {#item}

Empfehlungen aussprechen, die darauf basieren, ähnliche Artikel wie ein Artikel zu finden, den der Benutzer anzeigt oder kürzlich angesehen hat.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Personen, die das ansahen, sahen auch dies an]
* [!UICONTROL Personen, die das ansahen, kauften dies]
* [!UICONTROL Personen, die das kauften, kauften dies]
* [!UICONTROL Elemente mit ähnlichen Attributen]

**Entitätsparameter erforderlich**

* `entity.id` oder ein beliebiges Profilattribut, das als Schlüssel verwendet wird

**Lesungen**

* [Artikelbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.10: Benutzerbasierte Kriterien {#user}

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

## 1.11: Benutzerdefinierte Kriterien {#custom}

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

## 1.12: Geben Sie in Einschlussregeln verwendete Attribute an {#inclusion}

+++Siehe Details

**Lesungen**

* [Verwenden dynamischer und statischer Einschlussregeln](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.13: Ausgeschlossene IDs angeben {#exclude}

Übergeben Sie Entitäts-IDs für Entitäten, die Sie aus Ihren Empfehlungen ausschließen möchten. Beispielsweise können Sie Artikel ausschließen, die sich bereits im Warenkorb befinden.

+++Siehe Details

**Lesungen**

* [Kann ich eine Entität dynamisch ausschließen?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.14: Übergeben Sie die `entity.event.detailsOnly=true` parameter {#true}

Verwenden Sie Entitätsattribute, um Produkt- oder Inhaltsinformationen an [!DNL Target Recommendations].

+++Siehe Details

**Lesungen**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.15: Remote-Daten-Mapping (Remote) konfigurieren

Dieser Schritt stellt sicher, dass alle Daten, die an gesendet werden müssen [!DNL Target] festgelegt ist.

+++Siehe Details

![Diagramm zur Remote-Datenzuordnung](/help/dev/patterns/recs-atjs/assets/remote-data-mapping.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte alle Daten enthalten, die an gesendet werden müssen. [!DNL Target].

**Einrichten von Datenanbietern**

Weitere Informationen finden Sie unter [Datenanbieter](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lesungen**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die `targetPageParams()` -Funktion zum Festlegen aller erforderlichen Daten, die an gesendet werden müssen [!DNL Target].

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.16: at.js laden {#web}

Dieser Schritt stellt sicher, dass die JavaScript-Bibliothek at.js geladen und initialisiert wird.

+++Siehe Details

![Adobe Target Web SDK-Diagramm laden](/help/dev/patterns/recs-atjs/assets/load-web-sdk.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Laden Sie das Digital Marketing-Team herunter oder fragen Sie es nach dem `at.js 2.*x*` JavaScript-Bibliotheksdatei.

*Lesungen*

* [Funktionsweise von Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Funktionsweise von „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementieren von Target ohne einen Tag-Manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Aktionen**

Betten Sie die at.js-Datei auf allen Ihren Webseiten ein, auf denen Experimente, Optimierung, Personalisierung und Datenerfassung durchgeführt werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)





























