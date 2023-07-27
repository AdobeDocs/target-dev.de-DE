---
title: Zielgruppen-Targeting
description: Mit Zielgruppen können Sie Ihre Experimentierungs- und Personalisierungsaktivitäten auswählen. [!DNL Adobe Target] unterstützt standardmäßig unzählige leistungsstarke Zielgruppen-Targeting-Funktionen.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 21%

---

# Zielgruppen-Targeting

## Überblick

Mit Zielgruppen können Sie Ihre Experimentierungs- und Personalisierungsaktivitäten auswählen. [!DNL Adobe Target] unterstützt standardmäßig unzählige leistungsstarke Zielgruppen-Targeting-Funktionen. Die folgenden Attribute stehen zur Verfügung für [Zielgruppen-Targeting](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html):

### [!DNL Target] Bibliothek

Weitere Informationen finden Sie unter [[!DNL Target] Bibliothek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html). &#x200B;
* Verwiesen von Bing
* Chrome-Browser
* Firefox-Browser
* Verwiesen von Google
* Internet Explorer
* Linux-Betriebssystem
* Mac OS-Betriebssystem
* Neue Besucher
* Zurückkehrende Besucher
* Safari-Browser
* Tablet-Computer
* Windows-Betriebssystem
* Verwiesen von Yahoo

### Geo

Weitere Informationen finden Sie unter [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).
&#x200B;&#x200B;
* Land/Region
* Land
* Stadt
* Postleitzahl
* Breitengrad
* Längengrad
* DMA
* Mobilnetzbetreiber

### Netzwerk

Weitere Informationen finden Sie unter [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html).

* ISP
* Domänenname
* Verbindungsgeschwindigkeit

### Mobile

Weitere Informationen finden Sie unter [Mobilgeräte](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html).

* Gerätemarketingbezeichnung
* Gerätemodell
* Gerätehersteller
* Ist Mobilgerät
* Ist Mobiltelefon
* Ist Tablet
* Betriebssystem
* Bildschirmhöhe (px)
* Bildschirmbreite (px)

### Benutzerspezifisch

Weitere Informationen finden Sie unter [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html).

* beliebiges Schlüssel-/Wertpaar

### Betriebssystem

Weitere Informationen finden Sie unter [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html).

* Linux
* Macintosh
* Windows

### Seiten der Site

Weitere Informationen finden Sie unter [Site-Seiten](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html).

* Aktuelle Seite
* Vorherige Seite
* Landingpage
* HTTP-Header

### Browser

Weitere Informationen finden Sie unter [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html).

* Typ
* Sprache 
* Version 

### Besucherprofil

Weitere Informationen finden Sie unter [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

* beliebiges Schlüssel/Wert-Paar, das beibehalten wird

### Traffic-Quelle

Weitere Informationen finden Sie unter [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html).

* Von Baidu
* Von Bing
* Von Google
* Von Yahoo
* Verweis-Landingpage: URL
* Verweis-Landingpage: Domain
* Verweis-Landingpage: Abfrage

### Zeitrahmen

Weitere Informationen finden Sie unter [Zeitraum.](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html)

* Startdatum / Enddatum

## Client-Hinweise

[!DNL Adobe Target] erfordert Client Hints für die korrekte Segmentierung der Zielgruppenattribute von Browser, Betriebssystem und Mobil sowie bestimmter Instanzen von Profilskripten. Weitere Hintergrundinformationen finden Sie unter [Benutzeragent und Client-Hinweise](../../../client-side/atjs/user-agent-and-client-hints.md).

### Übergeben von Client-Hinweisen an [!DNL Adobe Target]

Ab Node.js SDK v2.4.0 und Java SDK v2.3.0 können Client-Hinweise an gesendet werden. [!DNL Target] via `getOffers()` -Aufrufe. Client-Hinweise sollten im `request.context` -Objekt zusammen mit dem Benutzeragenten.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB Java-SDK]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## Geräteinterne Entscheidungsfindung

Die folgende Tabelle zeigt, welche Zielgruppenregeln für die Entscheidungsfindung auf dem Gerät unterstützt oder nicht unterstützt werden.

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

### Geotargeting für Entscheidungen auf Geräten

Um eine nahezu Nulllatenz für Entscheidungsaktivitäten auf dem Gerät mit geo-basierten Zielgruppen zu gewährleisten, empfiehlt Adobe, die Geowerte selbst im -Aufruf an anzugeben. `getOffers`. Legen Sie dazu die `Geo` -Objekt im `Context` des Antrags. Dies bedeutet, dass Ihr Server eine Möglichkeit benötigt, den Standort der einzelnen Endbenutzer zu ermitteln. Beispielsweise kann Ihr Server mithilfe eines von Ihnen konfigurierten Dienstes eine IP-zu-Geo-Suche durchführen. Einige Hosting-Provider, wie z. B. Google Cloud, bieten diese Funktionalität über benutzerdefinierte Header in jedem `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```js {line-numbers="true"}
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

>[!TAB Java-SDK]

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

Wenn Sie jedoch nicht die Möglichkeit haben, IP-zu-Geo-Suchen auf Ihrem Server durchzuführen, aber dennoch eine geräteübergreifende Entscheidungsfindung für `getOffers` Anforderungen, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, die zu jedem `getOffers` aufrufen. Diese Latenz sollte kleiner als eine Remote-Latenz sein. `getOffers` aufrufen, da es ein CDN trifft, das sich in der Nähe Ihres Servers befindet. Sie müssen **only** bereitstellen `ipAddress` im Feld `Geo` -Objekt im `Context` Ihrer Anfrage verwenden, damit das SDK den geografischen Standort der IP-Adresse Ihres Benutzers abrufen kann. Wenn ein anderes Feld zusätzlich zum `ipAddress` wird angegeben, [!DNL Target] Das SDK ruft die Metadaten für den geografischen Standort nicht zur Auflösung ab.

>[!BEGINTABS]

>[!TAB Node.js-SDK]

```js {line-numbers="true"}
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

>[!TAB Java-SDK]

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

## Serverseitige Entscheidungsfindung

Die folgende Tabelle zeigt, welche Zielgruppenregeln für serverseitige Entscheidungen unterstützt oder nicht unterstützt werden.

| Zielgruppenregel | Serverseitige Entscheidungsfindung |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Ja |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Ja |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Ja |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Ja |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager) | Ja |
