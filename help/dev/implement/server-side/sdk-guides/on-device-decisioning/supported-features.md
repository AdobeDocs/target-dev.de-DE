---
title: Welche Funktionen werden bei der Entscheidungsfindung auf dem Gerät unterstützt?
description: Erfahren Sie, wie Sie mithilfe eines Live-Server-Aufrufs die relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen bereitstellen können.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---

# Übersicht über unterstützte Funktionen

[!DNL Adobe Target]Die Server-seitigen SDKs von geben Entwicklern die Flexibilität, sich für Entscheidungen zwischen Leistung und Aktualisierung von Daten zu entscheiden. Sollte Ihnen also die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen am wichtigsten sein, sollte ein Live-Server-Aufruf durchgeführt werden. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät getroffen werden. Für [!UICONTROL on-device decisioning] Informationen zur Verwendung finden Sie in der folgenden Liste unterstützter Funktionen:

* Aktivitätstypen
* Zielgruppen-Targeting
* Zuordnungsmethode

## Aktivitätstypen 

Die folgende Tabelle zeigt, [Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) erstellt mithilfe der [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) werden unterstützt oder nicht unterstützt für [!UICONTROL on-device decisioning].

| Aktivitätstyp | Unterstützt |
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

Die folgende Tabelle zeigt, für welche Zielgruppenregeln unterstützt oder nicht unterstützt werden [!UICONTROL on-device decisioning].

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
| [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager) | Nein |

### Geotargeting für [!UICONTROL on-device decisioning]

Um eine nahezu Nulllatenz für [!UICONTROL on-device decisioning] -Aktivitäten mit geo-basierten Zielgruppen verwenden, empfiehlt Adobe, die Geowerte selbst im -Aufruf an anzugeben. `getOffers`. Legen Sie dazu die `Geo` -Objekt im `Context` des Antrags. Dies bedeutet, dass Ihr Server eine Möglichkeit benötigt, den Standort der einzelnen Endbenutzer zu ermitteln. Beispielsweise kann Ihr Server mithilfe eines von Ihnen konfigurierten Dienstes eine IP-zu-Geo-Suche durchführen. Einige Hosting-Provider, wie z. B. Google Cloud, bieten diese Funktionalität über benutzerdefinierte Header in jedem `HttpServletRequest`.

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

>[!TAB Java ]

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

Wenn Sie jedoch nicht die Möglichkeit haben, IP-zu-Geo-Suchen auf Ihrem Server durchzuführen, aber dennoch [!UICONTROL on-device decisioning] für `getOffers` Anforderungen, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, die zu jedem `getOffers` aufrufen. Diese Latenz sollte kleiner als eine Remote-Latenz sein. `getOffers` aufrufen, da es ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Sie dürfen nur die Variable `ipAddress` im Feld `Geo` -Objekt im `Context` Ihrer Anfrage verwenden, damit das SDK den geografischen Standort der IP-Adresse Ihres Benutzers abrufen kann. Wenn ein anderes Feld zusätzlich zum `ipAddress` wird angegeben, [!DNL Target] Das SDK ruft die Metadaten für den geografischen Standort nicht zur Auflösung ab.


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

>[!TAB Java ]

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

Die folgende Tabelle zeigt, welche Zuordnungsmethoden unterstützt oder nicht unterstützt werden [!UICONTROL on-device decisioning].

| Zuordnungsmethode | Unterstützt |
| --- | --- |
| Manuell | Ja |
| [Automatisch dem besten Erlebnis zuordnen](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Nein |
| [Automatisches Targeting für personalisierte Erlebnisse](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Nein |
