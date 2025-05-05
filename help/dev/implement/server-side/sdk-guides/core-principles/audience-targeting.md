---
title: Zielgruppen-Targeting
description: Zielgruppen können verwendet werden, um Ihre Experimentier- und Personalisierungsaktivitäten anzusprechen. [!DNL Adobe Target] unterstützt standardmäßig eine Vielzahl leistungsstarker Zielgruppen-Targeting-Funktionen.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 26%

---

# Zielgruppen-Targeting

## Überblick

Zielgruppen können verwendet werden, um Ihre Experimentier- und Personalisierungsaktivitäten anzusprechen. [!DNL Adobe Target] unterstützt standardmäßig eine Vielzahl leistungsstarker Zielgruppen-Targeting-Funktionen. Die folgenden Attribute sind für [Zielgruppen-Targeting](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html?lang=de) verfügbar:

### [!DNL Target]

Weitere Informationen finden Sie unter [[!DNL Target] Bibliothek](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html?lang=de).
&#x200B;
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

Weitere Informationen finden Sie unter [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=de).
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

Weitere Informationen finden Sie unter [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=de).

* ISP
* Domänenname
* Verbindungsgeschwindigkeit

### Mobile

Weitere Informationen finden Sie unter [Mobilgeräte](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=de).

* Gerätemarketingbezeichnung
* Gerätemodell
* Gerätehersteller
* Ist Mobilgerät
* Ist Mobiltelefon
* Ist Tablet
* Betriebssystem
* Bildschirmhöhe (px)
* Bildschirmbreite (px)

### Benutzerdefiniert

Weitere Informationen finden Sie unter [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=de).

* Beliebiges Schlüssel/Wert-Paar

### Betriebssystem

Weitere Informationen finden Sie unter [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=de).

* Linux
* Macintosh
* Windows

### Seiten der Site

Weitere Informationen finden Sie unter [Site-Seiten](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=de).

* Aktuelle Seite
* Vorherige Seite
* Landingpage
* HTTP-Header

### Browser

Weitere Informationen finden Sie unter [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=de).

* Typ
* Sprache 
* Version 

### Besucherprofil

Weitere Informationen finden Sie unter [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de).

* Beliebiges Schlüssel/Wert-Paar, das beibehalten wird

### Traffic-Quelle

Weitere Informationen finden Sie unter [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=de).

* Von Baidu
* Von Bing
* Von Google
* Von Yahoo
* Verweis-Landingpage: URL
* Verweis-Landingpage: Domain
* Verweis-Landingpage: Abfrage

### Zeitrahmen

Weitere Informationen finden Sie unter [Zeitraum](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=de).

* Startdatum / Enddatum

## Client-Hinweise

[!DNL Adobe Target] erfordert Client Hints für die korrekte Segmentierung von Browser-, Betriebssystem- und mobilen Zielgruppenattributen sowie bestimmte Instanzen von Profilskripten. Weitere Hintergrundinformationen finden Sie unter [Benutzeragent und Client Hints](../../../client-side/atjs/user-agent-and-client-hints.md).

### Weitergeben von Client Hints an [!DNL Adobe Target]

Ab Node.js SDK v2.4.0 und Java SDK v2.3.0 können Client Hints über `getOffers()`-Aufrufe an [!DNL Target] gesendet werden. Client-Hinweise sollten zusammen mit dem Benutzeragenten im `request.context`-Objekt enthalten sein.

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

>[!TAB Java SDK]

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

Die folgende Tabelle gibt an, welche Zielgruppenregeln für die geräteinterne Entscheidungsfindung unterstützt oder nicht unterstützt werden.

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

### Geotargeting für On-Device Decisioning

Um bei Entscheidungsaktivitäten auf dem Gerät mit geobasierten Zielgruppen eine Latenz nahe Null beizubehalten, empfiehlt Adobe, die Geowerte selbst in dem Aufruf an `getOffers` anzugeben. Legen Sie dazu das `Geo`-Objekt im `Context` der Anfrage fest. Das bedeutet, dass Ihr Server eine Möglichkeit benötigt, den Standort jedes Endbenutzers zu bestimmen. Ihr Server kann beispielsweise mithilfe eines von Ihnen konfigurierten Services eine IP-zu-Geo-Suche durchführen. Einige Hosting-Anbieter wie Google Cloud bieten diese Funktion über benutzerdefinierte Header in jedem `HttpServletRequest`.

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

>[!TAB Java SDK]

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

Wenn Sie jedoch nicht über die Möglichkeit verfügen, auf Ihrem Server IP-zu-Geo-Suchen durchzuführen, aber dennoch Entscheidungsfindungen auf dem Gerät für `getOffers`-Anfragen durchführen möchten, die geobasierte Zielgruppen enthalten, wird dies ebenfalls unterstützt. Der Nachteil dieses Ansatzes besteht darin, dass eine Remote-IP-zu-Geo-Suche verwendet wird, wodurch zu jedem `getOffers`-Aufruf eine Latenz hinzukommt. Diese Latenz sollte niedriger sein als eine Remote-`getOffers`, da sie ein CDN berührt, das sich in der Nähe Ihres Servers befindet. Sie müssen **nur** das Feld `ipAddress` im `Geo` in der `Context` Ihrer Anfrage angeben, damit die SDK den geografischen Standort der IP-Adresse Ihres Benutzers abrufen kann. Wenn zusätzlich zum `ipAddress` ein anderes Feld bereitgestellt wird, ruft der [!DNL Target] SDK die Geolokalisierungsmetadaten nicht zur Auflösung ab.

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

>[!TAB Java SDK]

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

## Server-seitige Entscheidungsfindung

Die folgende Tabelle gibt an, welche Zielgruppenregeln für die Server-seitige Entscheidungsfindung unterstützt oder nicht unterstützt werden.

| Zielgruppenregel | Server-seitige Entscheidungsfindung |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=de) | Ja |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=de) | Ja |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=de) | Ja |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=de) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=de) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=de) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=de) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de) | Ja |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=de) | Ja |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=de) | Ja |
| [Experience Cloud-Zielgruppen](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=de) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager | Ja |
