---
title: Welche Funktionen werden bei der Entscheidungsfindung auf dem Gerät unterstützt?
description: Erfahren Sie, wie Sie mithilfe eines Live-Server-Aufrufs die relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen bereitstellen können.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---

# Übersicht über unterstützte Funktionen

Die serverseitigen SDKs von [!DNL Adobe Target] geben Entwicklern die Flexibilität, zwischen Leistung und Aktualisierung von Daten für Entscheidungen zu wählen. Sollte Ihnen also die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen am wichtigsten sein, sollte ein Live-Server-Aufruf durchgeführt werden. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät getroffen werden. Damit [!UICONTROL on-device decisioning] funktioniert, lesen Sie die folgende Liste unterstützter Funktionen:

* Aktivitätstypen
* Zielgruppen-Targeting
* Zuordnungsmethode

## Aktivitätstypen 

Die folgende Tabelle zeigt, welche [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), die mit dem [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) erstellt wurden, für [!UICONTROL on-device decisioning] unterstützt oder nicht unterstützt werden.

| Aktivitätstyp | „Unterstützt“ |
| --- | --- |
| [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Ja |
| [Automatische Zuordnung](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Nein |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | Ja |
| [Multivariate Tests](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Nein |
| [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Ja |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | Nein |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | Nein |


## Zielgruppen-Targeting

Die folgende Tabelle zeigt, welche Zielgruppenregeln für [!UICONTROL on-device decisioning] unterstützt werden oder nicht.

| Zielgruppenregel | Gerätebezogene Entscheidungsfindung |
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
| [Experience Cloud-Zielgruppen](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager) | Nein |

### Geotargeting für [!UICONTROL on-device decisioning]

Um eine nahezu Nulllatenz für [!UICONTROL on-device decisioning] -Aktivitäten mit geo-basierten Zielgruppen zu gewährleisten, empfiehlt Adobe, die Geowerte selbst im Aufruf von `getOffers` anzugeben. Setzen Sie dazu das Objekt `Geo` in das Objekt `Context` der Anfrage. Dies bedeutet, dass Ihr Server eine Möglichkeit benötigt, den Standort der einzelnen Endbenutzer zu ermitteln. Beispielsweise kann Ihr Server mithilfe eines von Ihnen konfigurierten Dienstes eine IP-zu-Geo-Suche durchführen. Einige Hosting-Provider, wie z. B. Google Cloud, stellen diese Funktionalität über benutzerdefinierte Header in jedem `HttpServletRequest` bereit.

>[!BEGINTABS]

>[!TAB node.js]

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

Wenn Sie jedoch keine IP-zu-Geo-Suchen auf Ihrem Server durchführen können, aber dennoch [!UICONTROL on-device decisioning] für `getOffers` -Anforderungen ausführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, wodurch jedem `getOffers` -Aufruf Latenzzeiten hinzugefügt werden. Diese Latenz sollte kleiner als ein Remote-Aufruf von `getOffers` sein, da er ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Sie dürfen das Feld `ipAddress` nur im Objekt `Geo` in der `Context` Ihrer Anfrage angeben, damit das SDK den geografischen Standort der IP-Adresse Ihres Benutzers abruft. Wenn ein anderes Feld zusätzlich zum `ipAddress` angegeben wird, ruft das [!DNL Target]-SDK die Metadaten für den geografischen Standort nicht zur Auflösung ab.


>[!BEGINTABS]

>[!TAB node.js]

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

Die folgende Tabelle zeigt, welche Zuordnungsmethoden für [!UICONTROL on-device decisioning] unterstützt werden oder nicht.

| Zuordnungsmethode | „Unterstützt“ |
| --- | --- |
| Manuell | Ja |
| [Automatisch dem besten Erlebnis zuordnen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Nein |
