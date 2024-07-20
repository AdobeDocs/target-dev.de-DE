---
keywords: Implementierung, JavaScript-Bibliothek, JS, at.js, Entscheidungsfindung auf dem Gerät, Geräteentscheidung, unterstützte Funktionen, 8 USD
description: Erfahren Sie, welche Funktionen für [!UICONTROL on-device decisioning] unterstützt werden.
title: Welche Funktionen werden bei der On-Device-Entscheidungsfindung unterstützt?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 12%

---

# Unterstützte Funktionen für [!UICONTROL on-device decisioning]

Das JS-SDK [!DNL Adobe Target] gibt Kunden die Möglichkeit, für Entscheidungen zwischen Leistung und Aktualisierung von Daten zu wählen. Sollte Ihnen also die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen am wichtigsten sein, sollte ein Live-Server-Aufruf durchgeführt werden. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät und im Speicher getroffen werden. Damit [!UICONTROL on-device decisioning] funktioniert, lesen Sie die folgenden Abschnitte, in denen die unterstützten Funktionen aufgelistet sind.

## Unterstützte Aktivitätstypen

Die folgende Tabelle zeigt, welche [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), die vom [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) oder vom [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) erstellt wurden, für [!UICONTROL on-device decisioning] unterstützt oder nicht unterstützt werden.

| Aktivitätstyp | Unterstützt? |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Nein |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Nein |
| [Aktivitäten, die Analytics für Target verwenden](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Ja |

## Zielgruppen-Targeting

Die folgende Tabelle zeigt, welche Zielgruppenregeln für [!UICONTROL on-device decisioning] unterstützt werden oder nicht.

| Zielgruppenregel | Unterstützt? |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja<P>Bei der Verwendung der Entscheidungsfindung auf dem Gerät werden die folgenden Geo-Attribute unterstützt:<ul><li>Land/Region</li><li>Stadt</li><li>Breitengrad</li><li>Längengrad</li></ul> |
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

Um eine minimale Latenz für [!UICONTROL on-device decisioning] -Aktivitäten mit geo-basierten Zielgruppen zu gewährleisten, empfiehlt Adobe, die Geowerte selbst im Aufruf von [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) anzugeben. Legen Sie das Geo-Objekt im Kontext der Anforderung fest. Das bedeutet, dass der Browser die Position jedes Besuchers ermitteln kann. Sie können beispielsweise mithilfe eines von Ihnen konfigurierten Dienstes eine IP-zu-Geo-Suche durchführen. Einige Hosting-Provider, wie z. B. Google Cloud, stellen diese Funktionalität über benutzerdefinierte Header in jedem `HttpServletRequest` bereit.

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

Wenn Sie jedoch keine IP-zu-Geo-Suchen auf Ihrem Server durchführen können, aber dennoch [!UICONTROL on-device decisioning] für [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)-Anforderungen ausführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, wodurch jedem `getOffers` -Aufruf Latenzzeiten hinzugefügt werden. Diese Latenz sollte kleiner als ein `getOffers` -Aufruf mit serverseitiger Entscheidungsfindung sein, da es auf ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Geben Sie nur das Feld &quot;ipAddress&quot;im Geo-Objekt im Kontext Ihrer SDK-Anfrage an, um den geografischen Standort der IP-Adresse Ihres Besuchers abzurufen. Wenn ein anderes Feld zusätzlich zur &quot;ipAddress&quot;bereitgestellt wird, ruft das [!DNL Target]-SDK die Metadaten für den geografischen Standort nicht zur Auflösung ab.

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

Die folgende Tabelle zeigt, welche Zuordnungsmethoden für [!UICONTROL on-device decisioning] unterstützt werden oder nicht.

| Zuordnungsmethode | Unterstützt? |
| --- | --- |
| Manuell | Ja |
| [Automatisch dem besten Erlebnis zuordnen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Nein |
