---
title: Welche Funktionen werden bei der geräteinternen Entscheidungsfindung unterstützt?
description: Erfahren Sie, wie Sie mithilfe eines Live-Server-Aufrufs relevante und ansprechendste personalisierte Inhalte über maschinelles Lernen bereitstellen können.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
TQID: https://experienceleague.adobe.com/Fgwu8Nh90i-tS1aCUVmQReGz6DYBP2GHdcNM7z17BSk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 731
ht-degree: 9%

---

# Übersicht über die unterstützten Funktionen

Die Server-seitigen SDKs von [!DNL Adobe Target] bieten Entwicklern die Flexibilität, bei Entscheidungen zwischen Leistung und Aktualität der Daten zu wählen. Mit anderen Worten: Wenn die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen für Sie am wichtigsten ist, sollte ein Live-Server-Aufruf erfolgen. Wenn die Leistung jedoch kritischer ist, sollte eine geräteinterne Entscheidung getroffen werden. Informationen [!UICONTROL &#x200B; Funktionsfähigkeit von &#x200B;]On-Device Decisioning“ finden Sie in der folgenden Liste unterstützter Funktionen:

* Aktivitätstypen
* Zielgruppen-Targeting
* Zuordnungsmethode

## Aktivitätstypen

Die folgende Tabelle gibt an, welche [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de) die mit dem [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de&) erstellt wurden, für die Entscheidungsfindung [!UICONTROL &#x200B; Gerät unterstützt oder nicht &#x200B;].

| Aktivitätstyp | „Unterstützt“ |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=de) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=de) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=de) | Nein |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de) (A4T) | Ja |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=de) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=de) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=de) (AP) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=de) | Nein |


## Zielgruppen-Targeting

Die folgende Tabelle gibt an, welche Zielgruppenregeln für die Entscheidungsfindung [!UICONTROL &#x200B; Gerät unterstützt oder nicht &#x200B;] werden.

| Zielgruppenregel | On-device Decisioning |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=de) | Ja |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=de) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=de) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=de) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=de) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=de) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=de) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=de) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=de) | Ja |
| [Experience Cloud-Zielgruppen](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=de) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager | Nein |

### Geotargeting für [!UICONTROL On-Device Decisioning]

Um bei Aktivitäten mit [!UICONTROL -basierten Zielgruppen eine Latenz von nahezu null für &#x200B;] Entscheidungsfindung auf dem Gerät beizubehalten, empfiehlt Adobe, die Geowerte selbst in dem Aufruf an `getOffers` anzugeben. Legen Sie dazu das `Geo`-Objekt im `Context` der Anfrage fest. Das bedeutet, dass Ihr Server eine Möglichkeit benötigt, den Standort jedes Endbenutzers zu bestimmen. Ihr Server kann beispielsweise mithilfe eines von Ihnen konfigurierten Services eine IP-zu-Geo-Suche durchführen. Einige Hosting-Anbieter wie Google Cloud bieten diese Funktion über benutzerdefinierte Header in jedem `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

Wenn Sie jedoch nicht über die Möglichkeit verfügen, auf Ihrem Server IP-zu-Geo-Suchen durchzuführen, aber dennoch [!UICONTROL On-Device Decisioning] für `getOffers`-Anfragen durchführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, wodurch zu jedem `getOffers`-Aufruf eine Latenz hinzukommt. Diese Latenz sollte niedriger sein als eine Remote-`getOffers`, da sie ein CDN berührt, das sich in der Nähe Ihres Servers befindet. Sie müssen das Feld `ipAddress` im `Geo` nur im `Context` Ihrer Anfrage angeben, damit die SDK den geografischen Standort der IP-Adresse Ihres Benutzers abrufen kann. Wenn zusätzlich zum `ipAddress` ein anderes Feld bereitgestellt wird, ruft der [!DNL Target] SDK die Geolokalisierungsmetadaten nicht zur Auflösung ab.


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## Zuordnungsmethode

Die folgende Tabelle gibt an, welche Zuordnungsmethoden für die [!UICONTROL On-Device Decisioning“ unterstützt oder nicht &#x200B;] werden.

| Zuordnungsmethode | „Unterstützt“ |
| --- | --- |
| Manuell | Ja |
| [Automatische Zuordnung zu bestem Erlebnis](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=de) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html?lang=de) | Nein |
