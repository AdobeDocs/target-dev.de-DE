---
keywords: Implementierung, JavaScript-Bibliothek, JS, ATJS, On-Device Decisioning, On-Device Decisioning, Unterstützte Funktionen, $8
description: Erfahren Sie, welche Funktionen für [!UICONTROL On-Device Decisioning] unterstützt werden.
title: Welche Funktionen bei der geräteinternen Entscheidungsfindung unterstützt werden
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
TQID: https://experienceleague.adobe.com/ummFURb6WnrNCbiQNDtzWmtZq05am9CMn9UXL0SPaXo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 235baadf4059d2c363368408012630d6619aef99
workflow-type: tm+mt
source-wordcount: 747
ht-degree: 8%

---

# Unterstützte Funktionen für [!UICONTROL On-Device Decisioning]

Die [!DNL Adobe Target] JS-SDK bietet Kundinnen und Kunden die Flexibilität, bei Entscheidungen zwischen Leistung und Aktualität der Daten zu wählen. Mit anderen Worten: Wenn die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen für Sie am wichtigsten ist, sollte ein Live-Server-Aufruf erfolgen. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät und im Arbeitsspeicher getroffen werden. Damit [!UICONTROL On-Device Decisioning] funktioniert, lesen Sie die folgenden Abschnitte, in denen die unterstützten Funktionen aufgeführt sind.

## Unterstützte Aktivitätstypen

Die folgende Tabelle gibt an, welche [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de), die vom [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de) oder [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de) (VEC) erstellt wurden, für [!UICONTROL &#x200B; Entscheidungsfindung auf dem Gerät unterstützt oder nicht unterstützt werden].

| Aktivitätstyp | Unterstützt? |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=de) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=de) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=de) ![Premium](../../../assets/premium.png) | Nein |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=de) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=de) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=de) ![Premium](../../../assets/premium.png) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=de) ![Premium](../../../assets/premium.png) | Nein |
| [Aktivitäten mit Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de&) (A4T) | Ja |

## Zielgruppen-Targeting

Die folgende Tabelle gibt an, welche Zielgruppenregeln für die Entscheidungsfindung [!UICONTROL &#x200B; Gerät unterstützt oder nicht &#x200B;] werden.

| Zielgruppenregel | Unterstützt? |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=de) | Ja<P>Bei der Verwendung der geräteinternen Entscheidungsfindung werden die folgenden Geoattribute unterstützt:<ul><li>Land/Region</li><li>Stadt</li><li>Breitengrad</li><li>Längengrad</li></ul> |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=de) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=de) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=de) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=de) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=de) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=de) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=de) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=de) | Ja |
| Adobe Experience Cloud-Zielgruppen<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] und [!DNL Adobe Experience Manager]) | Nein |

### Geotargeting für [!UICONTROL On-Device Decisioning]

Um bei Aktivitäten mit [!UICONTROL -basierten Zielgruppen eine minimale Latenz &#x200B;] Entscheidungsfindung auf dem Gerät zu erhalten, empfiehlt Adobe, die Geowerte selbst in dem Aufruf von [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) anzugeben. Legen Sie das Geo-Objekt im Kontext der Anfrage fest. Dies bedeutet, dass Sie über den Browser den Standort jedes Besuchers ermitteln können. Sie können beispielsweise mithilfe eines von Ihnen konfigurierten Services eine IP-zu-Geo-Suche durchführen. Einige Hosting-Anbieter wie Google Cloud bieten diese Funktion über benutzerdefinierte Header in jedem `HttpServletRequest`.

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

Wenn Sie jedoch keine IP-zu-Geo-Suchen auf Ihrem Server durchführen können, aber dennoch [!UICONTROL On-Device Decisioning] für [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)-Anfragen durchführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, die zu jedem `getOffers`-Aufruf eine Latenz hinzufügt. Diese Latenz sollte niedriger sein als ein `getOffers` Aufruf bei Server-seitiger Entscheidungsfindung, da sie auf ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Geben Sie im Geo-Objekt nur das Feld „ipAddress“ im Kontext Ihrer Anfrage an, dass die SDK den geografischen Standort der IP-Adresse Ihres Besuchers abruft. Wenn zusätzlich zur „IP-Adresse“ ein anderes Feld angegeben wird, ruft die [!DNL Target] SDK die Geolokalisierungs-Metadaten nicht zur Auflösung ab.

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

Die folgende Tabelle gibt an, welche Zuordnungsmethoden für die [!UICONTROL On-Device Decisioning“ unterstützt oder nicht &#x200B;] werden.

| Zuordnungsmethode | Unterstützt? |
| --- | --- |
| Manuell | Ja |
| [Automatische Zuordnung zu bestem Erlebnis](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=de) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=de) | Nein |



