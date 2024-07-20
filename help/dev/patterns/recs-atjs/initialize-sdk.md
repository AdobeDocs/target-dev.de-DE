---
title: Initialisieren von SDKs
description: Stellen Sie sicher, dass alle erforderlichen Schritte zum Laden der JavaScript-Bibliothek [!DNL Adobe Target] at.js in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 5%

---

# Initialisieren von SDKs

Führen Sie die Schritte im Diagramm *SDK initialisieren* aus, um sicherzustellen, dass alle erforderlichen Aufgaben zum Laden der JavaScript-Bibliothek &quot;[!DNL Adobe Target] at.js&quot;in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

## SDK-Diagramm initialisieren {#diagram}

Bei mehrseitigen Anwendungen erfolgt dieser Fluss jedes Mal, wenn die Seite neu geladen wird, oder der Besucher zu einer neuen Seite auf der Website navigiert.

>[!NOTE]
>
>Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten. Die Schrittnummern sind nicht in einer bestimmten Reihenfolge und spiegeln nicht die Reihenfolge der Schritte wider, die in der Benutzeroberfläche von [!DNL Target] beim Erstellen der Aktivität unternommen wurden.

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

Dieser Schritt stellt sicher, dass die `VisitorAPI.js` -Bibliothek ordnungsgemäß geladen, konfiguriert und initialisiert wird.

+++Siehe Details

![Besucher-API-SDK-Diagramm laden](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Um den Besucher-ID-/API-Dienst verwenden zu können, muss Ihr Unternehmen für die [!DNL Adobe Experience Cloud] freigeschaltet sein und über eine [!UICONTROL Organization ID] verfügen. Weitere Informationen finden Sie unter [Experience Cloud-Anforderungen: Organisations-ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} im Handbuch *ID-Dienst-Hilfe* .
* Sie benötigen die Datei &quot;`VisitorAPI.js`&quot;. Sie sollten diese Datei bereits haben, wenn Sie [!DNL Adobe Analytics] implementiert haben. Diese Datei kann auch über die Erweiterung [[!DNL Adobe Experience Platform] tags](https://experienceleague.adobe.com/docs/tags.html){target=_blank} hinzugefügt oder vom [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank} heruntergeladen werden.

**VisitorAPI.js konfigurieren und referenzieren**

Weitere Informationen finden Sie unter [Implementieren des Experience Cloud-Dienstes für Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Lesungen**

* [Experience Cloud Identity Service - Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Über den ID-Dienst](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies und der Experience Cloud Identity-Dienst](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Anfordern und Festlegen von IDs durch den Experience Cloud Identity-Dienst](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Grundlegendes zu ID-Synchronisierung und Übereinstimmungsraten](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Aktionen**

* Betten Sie die Datei &quot;`VisitorAPI.js`&quot; in Ihre Webseiten ein.
* Erfahren Sie mehr über die [verfügbaren Konfigurationen für den Besucher-ID/API-Dienst](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Nachdem die `VisitorAPI.js` -Datei geladen wurde, verwenden Sie die `Visitor.getInstance` -Methode, um mit den erforderlichen Konfigurationen zu initialisieren.
* Machen Sie sich mit den [verfügbaren Methoden](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank} vertraut.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.2: Festlegen der Kunden-ID {#set}

Dieser Schritt stellt sicher, dass die bekannten IDs (CRM-ID, Benutzer-ID usw.) Ihrer Besucher zur geräteübergreifenden Personalisierung mit der anonymen ID [!DNL Adobe] verknüpft sind.

+++Siehe Details

![Festlegen der Kunden-ID](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die bekannte ID der Besucher sollte auf der Datenschicht verfügbar sein.

**Festlegen der Kunden-ID**
Weitere Informationen finden Sie unter [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Lesungen**

* [Echtzeit-Profilsynchronisierung für mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Aktionen**

* Verwenden Sie `visitor.setCustomerIDs` , um die bekannte ID des Besuchers festzulegen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.3: Automatische Seitenladeanforderung konfigurieren {#automatic}

Dieser Schritt ermöglicht es at.js, alle Erlebnisse abzurufen, die beim Laden der JavaScript-Bibliotheksdatei at.js auf der Seite gerendert werden müssen.

+++Siehe Details

![Automatische Seitenladeanforderung konfigurieren](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Nicht alle Daten in der Datenschicht müssen an [!DNL Target] gesendet werden. Wenden Sie sich an Ihr Business-Team (Digital Marketing Team), um zu ermitteln, welche Daten für Experimente, Optimierung und Personalisierung nützlich sind. Nur diese Daten sollten an [!DNL Target] gesendet werden.
* Stellen Sie sicher, dass Sie keine personenbezogenen Daten (PII) an [!DNL Target] senden.

**Automatische Seitenladeanforderung konfigurieren**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Lesungen**

Erfahren Sie mehr über die Einstellung `pageLoadEnabled` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie das Objekt `window.targetGlobalSettings` , um automatische Seitenladeanfragen zu aktivieren.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.4: Flackern-Handhabung konfigurieren {#flicker}

Dieser Schritt stellt sicher, dass bei der Bereitstellung von Erlebnissen kein Seitenflackern auftritt.

+++Siehe Details

![Konfigurieren des Flackerbearbeitungsdiagramms](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Erfahren Sie mehr mit dem für die Webseitenleistung zuständigen Team über die Vor- und Nachteile der Flackerverhinderung mithilfe der von at.js verwendeten Standardmethode. Sie können nach Designmustern suchen, mit denen Sie benutzerdefinierte Flacker-Handling-Lösungen wie Lader-Animation verwenden können. Wenn Sie kein Muster finden, können Sie ein neues Muster anfordern.

**Konfigurieren der Flackerbearbeitung**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Durch Festlegen von `bodyHidingEnabled` auf `true` wird der gesamte Seitentext ausgeblendet, während die Seitenladeanforderung ausgeführt wird. Wenn Sie die automatische Seitenladeanforderung aus irgendeinem Grund nicht aktiviert haben (z. B. Daten später nicht mehr bereit), ist es am besten, diese Einstellung auf `false` festzulegen.

Wenn Sie `bodyHidingEnabled` deaktiviert haben, weil Sie APLR nicht auslösen möchten und die Seitenanforderung später auslösen möchten oder keine Flackerbehandlung benötigen, müssen Sie Ihre eigene Flackerbehandlung implementieren. Sie können das Flackern auf zwei Arten handhaben: das Ausblenden der zu prüfenden Abschnitte oder das Anzeigen einer Halbleiter für die zu testenden Abschnitte.

**Lesungen**

* [Verwaltung von Flackern mit „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Erfahren Sie mehr über die Objekte bodyHiddenStyle und bodyHidingEnabled in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie das Objekt `window.targetGlobalSettings` so, dass es `bodyHiddenStyle` und `bodyHidingEnabled` festlegt.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.5: Konfigurieren der Datenzuordnung {#data-mapping}

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Diagramm für die Datenzuordnung](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten fertig sein, die an [!DNL Target] gesendet werden müssen.
* Recommendations: Profil anreichern.
   * Übergeben Sie `entity.id` , um Daten zu kürzlich angezeigten Kriterien und Elementen basierend auf Kriterien zu erfassen, die auf dem zuletzt angezeigten Produkt basieren.
   * Übergeben Sie `entity.id` , um Daten für Beliebtheitskriterien basierend auf der Lieblingskategorie zu erfassen.
   * Übergeben Sie das Profilattribut, wenn benutzerdefinierte Kriterien darauf basieren oder in der Filterung von Einschlussregeln in beliebigen Kriterien verwendet werden.
* Recommendations: Erfassen Sie Produktdaten.
   * Andere (reservierte und benutzerdefinierte) Entitätsparameter können an die Erfassung oder Aktualisierung des Produktkatalogs in [!DNL Recommendations] übergeben werden.
   * Der Produktkatalog kann auch mithilfe von Entitäts-Feeds mit der [!DNL Target] -Benutzeroberfläche oder -API aktualisiert werden.

**Zuordnen von Daten zu[!DNL Target]**

Weitere Informationen finden Sie unter [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Lesungen**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planen und Implementieren von Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Recommendations-Katalog einrichten](/help/dev/implement/recommendations/recommendations.md)

**Aktionen**

* Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.6. Promotion {#promotion}

Fügen Sie Promotionsartikel hinzu und steuern Sie deren Platzierung in Ihren [!DNL Target Recommendations] [Designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Siehe Details

**Verfügbare Optionen**

* Hervorheben nach IDs
* [Hervorheben nach Sammlung](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Hervorheben nach Attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Erforderliche Entitätsparameter**

* Das Elementattribut in der Promotion muss bei Verwendung der Option &quot;Bewerben nach Attribut&quot;übergeben werden.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.7: Warenkorbbasierte Kriterien {#cart}

Machen Sie Empfehlungen basierend auf den Inhalten des Warenkorbs des Benutzers.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**Erforderliche Entitätsparameter**

* cartIds

**Lesungen**

* [Warenkorb-basiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.8: Beliebtheitsbasierte Kriterien {#popularity}

Machen Sie Empfehlungen basierend auf der allgemeinen Beliebtheit eines Artikels auf Ihrer Site oder auf der Beliebtheit von Artikeln in der bevorzugten oder am häufigsten angezeigten Kategorie, Marke, Genre usw. eines Benutzers.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**Erforderliche Entitätsparameter**

* `entity.categoryId` oder das Elementattribut für die Beliebtheit, wenn das Kriterium auf dem aktuellen Element oder dem Elementattribut basiert.
* Für die am häufigsten angezeigten/am häufigsten verkauften Artikel auf der Site muss nichts übergeben werden.

**Lesungen**

* [Beliebtheitsbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.9: Artikelbasierte Kriterien {#item}

Empfehlungen aussprechen, die darauf basieren, ähnliche Artikel wie ein Artikel zu finden, den der Benutzer anzeigt oder kürzlich angesehen hat.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Erforderliche Entitätsparameter**

* `entity.id` oder ein beliebiges Profilattribut, das als Schlüssel verwendet wird

**Lesungen**

* [Elementbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.10: Benutzerbasierte Kriterien {#user}

Empfehlungen basierend auf dem Benutzerverhalten erstellen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**Erforderliche Entitätsparameter**

* `entity.id`

**Lesungen**

* [Benutzerbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.11: Benutzerdefinierte Kriterien {#custom}

Machen Sie Empfehlungen basierend auf einer benutzerdefinierten Datei, die Sie hochladen.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL Custom algorithm]

**Erforderliche Entitätsparameter**

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

## 1.14: Übergeben des Parameters `entity.event.detailsOnly=true` {#true}

Verwenden Sie Entitätsattribute, um Produkt- oder Inhaltsinformationen an [!DNL Target Recommendations] zu übergeben.

+++Siehe Details

**Lesungen**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.15: Remote-Daten-Mapping (Remote) konfigurieren

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Diagramm zur Remote-Datenzuordnung](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten fertig sein, die an [!DNL Target] gesendet werden müssen.

**Einrichten von Datenanbietern**

Weitere Informationen finden Sie unter [Datenanbieter](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Lesungen**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.16: at.js laden {#web}

Dadurch wird sichergestellt, dass die JavaScript-Bibliothek at.js geladen und initialisiert wird.

+++Siehe Details

![Adobe Target at.js-Diagramm laden](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Laden Sie die JavaScript-Bibliotheksdatei herunter oder fragen Sie sie bei Ihrem Digital Marketing-Team nach.`at.js 2.*x*`

*Lesungen*

* [Funktionsweise von Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Funktionsweise von „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementieren von Target ohne einen Tag-Manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Aktionen**

Betten Sie die at.js-Datei auf allen Ihren Webseiten ein, auf denen Experimente, Optimierung, Personalisierung und Datenerfassung durchgeführt werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 2 fort: [Datensammlung konfigurieren](/help/dev/patterns/recs-atjs/data-collection.md).
