---
keywords: Implementierung, JavaScript-Bibliothek, JS, at.js, Entscheidungsfindung auf dem Gerät, Geräteentscheidung, unterstützte Funktionen, 8 USD
description: Erfahren Sie, für welche Funktionen [!UICONTROL on-device decisioning].
title: Welche Funktionen werden bei der On-Device-Entscheidungsfindung unterstützt?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 9%

---

# Unterstützte Funktionen für [!UICONTROL on-device decisioning]

Die [!DNL Adobe Target] Das JS-SDK bietet Kunden die Möglichkeit, für Entscheidungen zwischen Leistung und Aktualisierung von Daten zu wählen. Sollte Ihnen also die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen am wichtigsten sein, sollte ein Live-Server-Aufruf durchgeführt werden. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät und im Speicher getroffen werden. Für [!UICONTROL on-device decisioning] lesen, um zu arbeiten, lesen Sie die folgenden Abschnitte, in denen die unterstützten Funktionen aufgelistet sind.

## Unterstützte Aktivitätstypen

Die folgende Tabelle zeigt, [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) erstellt von der [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) oder [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) werden unterstützt oder nicht unterstützt für [!UICONTROL on-device decisioning].

| Aktivitätstyp | Unterstützt? |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Nein |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Nein |
| [Aktivitäten mit Analytics für Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Ja |

## Zielgruppen-Targeting

Die folgende Tabelle zeigt, für welche Zielgruppenregeln unterstützt oder nicht unterstützt werden [!UICONTROL on-device decisioning].

| Zielgruppenregel | Unterstützt? |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| Adobe Experience Cloud-Zielgruppen<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], und [!DNL Adobe Experience Manager]) | Nein |

### Geotargeting für [!UICONTROL on-device decisioning]

So halten Sie die minimale Latenz für [!UICONTROL on-device decisioning] -Aktivitäten mit geo-basierten Zielgruppen verwenden, empfiehlt Adobe, die Geowerte selbst im -Aufruf an anzugeben. [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Legen Sie das Geo-Objekt im Kontext der Anforderung fest. Das bedeutet, dass der Browser die Position jedes Besuchers ermitteln kann. Sie können beispielsweise mithilfe eines von Ihnen konfigurierten Dienstes eine IP-zu-Geo-Suche durchführen. Einige Hosting-Provider, wie z. B. Google Cloud, bieten diese Funktionalität über benutzerdefinierte Header in jedem `HttpServletRequest`.

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

Wenn Sie jedoch keine IP-zu-Geo-Suchen auf Ihrem Server durchführen können, aber dennoch [!UICONTROL on-device decisioning] für [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) Anforderungen, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, wodurch Latenzzeiten zu jedem `getOffers` aufrufen. Diese Latenz sollte kleiner sein als `getOffers` mit serverseitiger Entscheidungsfindung aufrufen, da es ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Geben Sie nur das Feld &quot;ipAddress&quot;im Geo-Objekt im Kontext Ihrer SDK-Anfrage an, um den geografischen Standort der IP-Adresse Ihres Besuchers abzurufen. Wenn ein anderes Feld zusätzlich zur &quot;ipAddress&quot;angegeben wird, wird die [!DNL Target] Das SDK ruft die Metadaten für den geografischen Standort nicht zur Auflösung ab.

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

Die folgende Tabelle zeigt, welche Zuordnungsmethoden unterstützt oder nicht unterstützt werden [!UICONTROL on-device decisioning].

| Zuordnungsmethode | Unterstützt? |
| --- | --- |
| Manuell | Ja |
| [Automatisch dem besten Erlebnis zuordnen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Nein |
