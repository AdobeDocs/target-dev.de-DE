---
title: SDKs initialisieren
description: Stellen Sie sicher, dass alle erforderlichen Schritte zum Laden  [!DNL Adobe Target]  JavaScript-Bibliothek „at.js“ in der richtigen Reihenfolge ausgeführt werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 5%

---

# SDKs initialisieren

Führen Sie die Schritte im *Initialisieren von SDK* aus, um sicherzustellen, dass alle erforderlichen Aufgaben zum Laden der [!DNL Adobe Target] JavaScript-Bibliothek „at.js“ in der richtigen Reihenfolge ausgeführt werden.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie im Vollbildmodus anzuzeigen.

## SDK-Initialisierungsdiagramm {#diagram}

Bei mehrseitigen Anwendungen erfolgt dieser Fluss jedes Mal, wenn die Seite neu geladen wird oder der Besucher zu einer neuen Seite auf der Website navigiert.

>[!NOTE]
>
>Die Schrittnummern in der folgenden Abbildung entsprechen den folgenden Abschnitten. Die Schrittnummern befinden sich in keiner bestimmten Reihenfolge und entsprechen nicht der Reihenfolge der Schritte, die in der [!DNL Target]-Benutzeroberfläche beim Erstellen der Aktivität ausgeführt wurden.

![SDKs initialisieren - Diagramm](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

Klicken Sie auf die folgenden Links, um zu den gewünschten Abschnitten zu navigieren:

* [1.1: Laden der Besucher-API SDK](#load)
* [1.2: Kunden-ID festlegen](#set)
* [1.3: Konfigurieren der automatischen Seitenladeanfrage](#automatic)
* [1.4: Konfigurieren der Flackerhandhabung](#flicker)
* [1.5: Konfigurieren der Datenzuordnung](#data-mapping)
* [1.6: Absatzförderung](#promotion)
* [1.7: Warenkorb-basierte Kriterien](#cart)
* [1.8: Beliebtheitsbasierte Kriterien](#popularity)
* [1.9: Auf Artikeln basierende Kriterien](#item)
* [1.10: Benutzerbasierte Kriterien](#user)
* [1.11: Benutzerdefinierte Kriterien](#custom)
* [1.12: Angabe der in Einschlussregeln verwendeten Attribute](#inclusion)
* [1.13: ExcludeIds angeben](#exclude)
* [1.14: Übergeben Sie den Parameter entity.event.detailsOnly=true](#true)
* [1.15: Konfigurieren der Remote-Datenzuordnung](#remote)
* [1.16: at.js laden](#web)

## 1.1: Laden der Besucher-API SDK {#load}

Mit diesem Schritt können Sie sicherstellen, dass die `VisitorAPI.js` Bibliothek ordnungsgemäß geladen, konfiguriert und initialisiert wird.

+++Siehe Details

![SDK-Diagramm zum Laden der Besucher-API](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Um den Besucher-ID-/API-Service verwenden zu können, muss Ihr Unternehmen für die [!DNL Adobe Experience Cloud] aktiviert sein und über eine [!UICONTROL Organization ID] verfügen. Weitere Informationen finden Sie unter [Experience Cloud-Anforderungen: Organisations](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank}ID im *Identity Service-*).
* Sie benötigen die `VisitorAPI.js`. Sie sollten diese Datei bereits haben, falls Sie sie implementiert [!DNL Adobe Analytics]. Diese Datei kann auch über die [[!DNL Adobe Experience Platform] Tags-Erweiterung](https://experienceleague.adobe.com/docs/tags.html){target=_blank} hinzugefügt oder aus dem [Adobe Analytics Code Manager heruntergeladen ](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**Konfigurieren und Verweisen auf VisitorAPI.js**

Weitere Informationen finden Sie unter [Implementieren des Experience Cloud-Service für Target](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**Messwerte**

* [Übersicht über den Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [Über den ID-Service](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookies und der Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Anfordern und Festlegen von IDs durch den Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [Grundlegendes zu ID-Synchronisierung und Übereinstimmungsraten](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**Aktionen**

* Einbetten der `VisitorAPI.js`-Datei auf Ihren Web-Seiten.
* Lesen Sie mehr über die [verfügbaren Konfigurationen für den Besucher-ID-/API-Service](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* Nachdem die `VisitorAPI.js` geladen wurde, verwenden Sie die `Visitor.getInstance` Methode , um mit den erforderlichen Konfigurationen zu initialisieren.
* Machen Sie sich mit den [verfügbaren Methoden](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank} vertraut.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.2: Kunden-ID festlegen {#set}

Dieser Schritt stellt sicher, dass die bekannten IDs Ihrer Besucher (CRM-ID, Benutzer-ID usw.) zur geräteübergreifenden Personalisierung mit der anonymen ID von [!DNL Adobe] verknüpft sind.

+++Siehe Details

![Kunden-ID festlegen](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die bekannte ID der Besucher sollte in der Datenschicht verfügbar sein.

**Kunden-ID festlegen**
Weitere Informationen finden Sie unter [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**Messwerte**

* [Echtzeit-Profilsynchronisierung für mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**Aktionen**

* Verwenden Sie `visitor.setCustomerIDs`, um die bekannte Besucher-ID festzulegen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.3: Konfigurieren der automatischen Seitenladeanfrage {#automatic}

Dieser Schritt ermöglicht at.js das Abrufen aller Erlebnisse, die auf der Seite gerendert werden müssen, während die at.js-JavaScript-Bibliotheksdatei geladen wird.

+++Siehe Details

![Konfigurieren der automatischen Seitenladeanfrage](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Nicht alle Daten in der Datenschicht müssen an [!DNL Target] gesendet werden. Beraten Sie sich mit Ihrem Business-Team (Digital-Marketing-Team), um festzustellen, welche Daten für Experimente, Optimierungen und Personalisierungen nützlich sind. Nur diese Daten sollten an [!DNL Target] gesendet werden.
* Stellen Sie sicher, dass Sie keine personenbezogenen Daten (PII) an [!DNL Target] senden.

**Konfigurieren der automatischen Seitenladeanfrage**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Messwerte**

Erfahren Sie mehr über die `pageLoadEnabled` in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie das `window.targetGlobalSettings`-Objekt, um automatische Seitenladeanfragen zu aktivieren.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.4: Konfigurieren der Flackerhandhabung {#flicker}

Mit diesem Schritt wird sichergestellt, dass beim Bereitstellen von Erlebnissen kein Seitenflackern auftritt.

+++Siehe Details

![Konfigurieren des Flimmerhandhabungsdiagramms](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Führen Sie mit dem für die Leistung der Web-Seite zuständigen Team eine Diskussion über die Vor- und Nachteile der Flimmerkontrolle mithilfe der von at.js verwendeten Standardmethode. Sie können nach Designmustern suchen, die Ihnen die Verwendung benutzerdefinierter Flimmerhandhabungslösungen ermöglichen, z. B. Loader-Animationen. Wenn Sie ein Muster nicht finden, können Sie ein neues Muster anfordern.

**Konfigurieren der Flackerhandhabung**

Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

Wenn Sie `bodyHidingEnabled` auf `true` setzen, wird der gesamte Seitentext ausgeblendet, während die Seitenladeanforderung ausgeführt wird. Wenn Sie die automatische Seitenladeanforderung aus irgendeinem Grund nicht aktiviert haben (z. B. weil die Daten später nicht bereit sind), ist es am besten, diese Einstellung auf `false` festzulegen.

Wenn Sie `bodyHidingEnabled` deaktiviert haben, weil Sie APLR nicht auslösen möchten und die Seitenanforderung später auslösen möchten, oder keine Flackerbehandlung benötigen, müssen Sie Ihre eigene Flackerbehandlung implementieren. Flackern lässt sich auf zwei Arten handhaben: durch Ausblenden der zu testenden Abschnitte oder durch Anzeigen eines Thrombers auf den zu testenden Abschnitten.

**Messwerte**

* [Verwaltung von Flackern mit „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* Erfahren Sie mehr über die Objekte bodyHiddenStyle und bodyHidingEnabled in [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**Aktionen**

* Ändern Sie das `window.targetGlobalSettings`-Objekt, um `bodyHiddenStyle` und `bodyHidingEnabled` festzulegen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.5: Konfigurieren der Datenzuordnung {#data-mapping}

Mit diesem Schritt stellen Sie sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Datenzuordnungsdiagramm](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten bereit sein, die an [!DNL Target] gesendet werden müssen.
* Recommendations: Profil anreichern.
   * Übergeben Sie `entity.id`, um Daten für kürzlich angezeigte Kriterien und Elemente basierend auf Kriterien zu erfassen, die auf dem zuletzt angezeigten Produkt basieren.
   * Übergeben Sie `entity.id`, um Daten für Beliebtheitskriterien basierend auf der bevorzugten Kategorie zu erfassen.
   * Übergeben Sie das Profilattribut, wenn benutzerdefinierte Kriterien darauf basieren oder bei der Filterung von Einschlussregeln in beliebigen Kriterien verwendet werden.
* Recommendations: Nehmen Sie Produktdaten auf.
   * Andere Entitätsparameter (reserviert und benutzerdefiniert) können übergeben werden, um den Produktkatalog in [!DNL Recommendations] aufzunehmen oder zu aktualisieren.
   * Der Produktkatalog kann auch mithilfe von Entitäts-Feeds aktualisiert werden, indem die [!DNL Target]-Benutzeroberfläche oder -API verwendet wird.

**Daten[!DNL Target]** zuordnen

Weitere Informationen finden Sie unter [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**Messwerte**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [Planen und Implementieren von Recommendations](/help/dev/implement/recommendations/recommendations.md)
* [Recommendations-Katalog einrichten](/help/dev/implement/recommendations/recommendations.md)

**Aktionen**

* Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.6: Absatzförderung {#promotion}

Fügen Sie hochgestufte Elemente hinzu und steuern Sie deren Platzierung in Ihren [!DNL Target Recommendations] [Designs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++Siehe Details

**Verfügbare Optionen**

* Nach IDs hochstufen
* [Nach Sammlung bewerben](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [Hochstufen nach Attribut](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**Entitätsparameter erforderlich**

* Das Elementattribut in der Promotion muss bei Verwendung der Option „Nach Attribut bewerben“ übergeben werden.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.7: Warenkorb-basierte Kriterien {#cart}

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

## 1.8: Beliebtheitsbasierte Kriterien {#popularity}

Empfehlungen auf der Grundlage der allgemeinen Popularität eines Elements auf Ihrer Website oder auf der Grundlage der Popularität von Elementen innerhalb der Lieblings- oder am häufigsten angezeigten Kategorie, Marke, Genre usw.

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

* `entity.categoryId` oder das Elementattribut für Beliebtheit, wenn das Kriterium auf dem aktuellen Element oder dem Elementattribut basiert.
* Nichts darf für Am häufigsten angezeigt/Am häufigsten verkauft auf der Website weitergegeben werden.

**Messwerte**

* [Beliebtheitsbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.9: Auf Artikeln basierende Kriterien {#item}

Empfehlungen aussprechen, die darauf basieren, ähnliche Elemente zu finden wie ein Element, das der Benutzer gerade anzeigt oder kürzlich angeschaut hat.

+++Siehe Details

**Verfügbare Kriterien**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**Entitätsparameter erforderlich**

* `entity.id` oder ein als Schlüssel verwendetes Profilattribut

**Messwerte**

* [Elementbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.10: Benutzerbasierte Kriterien {#user}

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

## 1.11: Benutzerdefinierte Kriterien {#custom}

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

## 1.12: Angabe der in Einschlussregeln verwendeten Attribute {#inclusion}

+++Siehe Details

**Messwerte**

* [Verwenden dynamischer und statischer Einschlussregeln](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.13: ExcludeIds angeben {#exclude}

Übergeben Sie Entitäts-IDs für Entitäten, die Sie aus Ihren Empfehlungen ausschließen möchten. Beispielsweise können Sie Artikel ausschließen, die sich bereits im Warenkorb befinden.

+++Siehe Details

**Messwerte**

* [Kann ich eine Entität dynamisch ausschließen?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.14: Übergeben Sie den `entity.event.detailsOnly=true` {#true}

Verwenden Sie Entitätsattribute, um Produkt- oder Inhaltsinformationen an [!DNL Target Recommendations] zu übergeben.

+++Siehe Details

**Messwerte**

* [Entitätsattribute](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.15: Konfigurieren der Remote-Datenzuordnung (remote)

Dieser Schritt stellt sicher, dass alle Daten, die an [!DNL Target] gesendet werden müssen, festgelegt sind.

+++Siehe Details

![Remote-Datenzuordnungsdiagramm](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Die Datenschicht sollte mit allen Daten bereit sein, die an [!DNL Target] gesendet werden müssen.

**Einrichten von Datenanbietern**

Weitere Informationen finden Sie unter [Datenanbieter](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**Messwerte**

[targetPageParams-Funktion](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**Aktionen**

Verwenden Sie die Funktion `targetPageParams()` , um alle erforderlichen Daten festzulegen, die an [!DNL Target] gesendet werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

## 1.16: at.js laden {#web}

Dieser Schritt stellt sicher, dass die at.js-JavaScript-Bibliothek geladen und initialisiert wird.

+++Siehe Details

![Laden des Adobe Target-Diagramms „at.js“](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**Voraussetzungen**

* Laden Sie die Bibliotheksdatei für `at.js 2.*x*` JavaScript herunter oder fragen Sie Ihr Digital-Marketing-Team.

*Messwerte*

* [Funktionsweise von Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [Funktionsweise von „at.js“](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [Implementieren von Target ohne einen Tag-Manager](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**Aktionen**

Betten Sie die Datei „at.js“ in alle Web-Seiten ein, auf denen Experimente, Optimierungen, Personalisierungen und Datenerfassungen durchgeführt werden müssen.

+++

[Kehren Sie zum Diagramm oben auf dieser Seite zurück.](#diagram)

Fahren Sie mit Schritt 2: [Konfigurieren der Datenerfassung](/help/dev/patterns/recs-atjs/data-collection.md) fort.
