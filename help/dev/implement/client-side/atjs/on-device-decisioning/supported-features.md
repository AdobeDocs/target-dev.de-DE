---
keywords: Implementierung, JavaScript-Bibliothek, JS, ATJS, On-Device Decisioning, On-Device Decisioning, Unterstützte Funktionen, $8
description: Erfahren Sie, welche Funktionen für [!UICONTROL on-device decisioning] unterstützt werden.
title: Welche Funktionen bei der geräteinternen Entscheidungsfindung unterstützt werden
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 12%

---

# Unterstützte Funktionen für [!UICONTROL on-device decisioning]

Die [!DNL Adobe Target] JS-SDK bietet Kundinnen und Kunden die Flexibilität, bei Entscheidungen zwischen Leistung und Aktualität der Daten zu wählen. Mit anderen Worten: Wenn die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen für Sie am wichtigsten ist, sollte ein Live-Server-Aufruf erfolgen. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät und im Arbeitsspeicher getroffen werden. Damit [!UICONTROL on-device decisioning] funktioniert, lesen Sie die folgenden Abschnitte, in denen die unterstützten Funktionen aufgelistet sind.

## Unterstützte Aktivitätstypen

Die folgende Tabelle gibt an, welche [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), die vom [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) oder [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) erstellt wurden, für [!UICONTROL on-device decisioning] unterstützt oder nicht unterstützt werden.

| Aktivitätstyp | Unterstützt? |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Nein |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Nein |
| [Aktivitäten mit Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Ja |

## Zielgruppen-Targeting

Die folgende Tabelle gibt an, welche Zielgruppenregeln für [!UICONTROL on-device decisioning] unterstützt oder nicht unterstützt werden.

| Zielgruppenregel | Unterstützt? |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja<P>Bei der Verwendung der geräteinternen Entscheidungsfindung werden die folgenden Geoattribute unterstützt:<ul><li>Land/Region</li><li>Stadt</li><li>Breitengrad</li><li>Längengrad</li></ul> |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| Adobe Experience Cloud-Zielgruppen<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] und [!DNL Adobe Experience Manager]) | Nein |

### Geotargeting für [!UICONTROL on-device decisioning]

Um eine minimale Latenz für [!UICONTROL on-device decisioning] Aktivitäten mit geobasierten Zielgruppen zu wahren, empfiehlt Adobe, die Geowerte selbst im Aufruf von [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) anzugeben. Legen Sie das Geo-Objekt im Kontext der Anfrage fest. Dies bedeutet, dass Sie über den Browser den Standort jedes Besuchers ermitteln können. Sie können beispielsweise mithilfe eines von Ihnen konfigurierten Services eine IP-zu-Geo-Suche durchführen. Einige Hosting-Anbieter wie Google Cloud bieten diese Funktion über benutzerdefinierte Header in jedem `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

Wenn Sie jedoch keine IP-zu-Geo-Suchen auf Ihrem Server durchführen können, aber dennoch [!UICONTROL on-device decisioning] für [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)-Anfragen durchführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, die zu jedem `getOffers`-Aufruf eine Latenz hinzufügt. Diese Latenz sollte niedriger sein als ein `getOffers` Aufruf bei Server-seitiger Entscheidungsfindung, da sie auf ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Geben Sie im Geo-Objekt nur das Feld „ipAddress“ im Kontext Ihrer Anfrage an, dass die SDK den geografischen Standort der IP-Adresse Ihres Besuchers abruft. Wenn zusätzlich zur „IP-Adresse“ ein anderes Feld angegeben wird, ruft die [!DNL Target] SDK die Geolokalisierungs-Metadaten nicht zur Auflösung ab.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### Zuordnungsmethode

Die folgende Tabelle gibt an, welche Zuordnungsmethoden für [!UICONTROL on-device decisioning] unterstützt oder nicht unterstützt werden.

| Zuordnungsmethode | Unterstützt? |
| --- | --- |
| Manuell | Ja |
| [Automatische Zuordnung zu bestem Erlebnis](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Nein |
