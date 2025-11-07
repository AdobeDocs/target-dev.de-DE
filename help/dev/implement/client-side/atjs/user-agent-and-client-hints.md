---
keywords: at.js, Browser-Benutzeragent, Benutzeragent, Client Hints, Benutzeragent
description: Erfahren Sie, wie Adobe Target den user-agent und Client Hints verwendet, um Besucher für die Segmentierung und Personalisierung zu qualifizieren.
title: User Agent und Client Hints
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 72%

---

# User-agent und Client Hints

Adobe Target verwendet den user-agent, um Besucher für die Segmentierung und Personalisierung zu qualifizieren.

>[!NOTE]
>
>Die Informationen in diesem Artikel gelten für [at.js-Version 2.9.0](target-atjs-versions.md) (oder höher).

Jedes Mal, wenn ein Webbrowser eine Anfrage an einen Server sendet, werden Informationen über den Browser und die Umgebung, in der der Browser ausgeführt wird, in die -Kopfzeile der Anfrage aufgenommen. Seit den frühen Tagen des Internets wurden diese Daten in einer Zeichenfolge zusammengefasst, dem sogenannten user-agent.

Der folgende Text ist ein Beispiel für einen user-agent eines Mac OS X-Computers, der einen Safari-Browser verwendet:

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

Von diesem user-agent kann der Server, der die Anfrage erhält, die folgenden Informationen zum Browser und Betriebssystem ableiten:

| Informationen | Details |
| --- | --- |
| Software-Name | Chrome |
| Software-Version | 101 |
| Vollständige Software-Version | 101.0.4951.41 |
| Name der Layout-Engine | AppleWebKit |
| Version der Layout-Engine | 537.36 |
| Betriebssystem | Android |
| Version des Betriebssystems | Android 12 (Snow Cone) |
| Gerät | SM-S908E (Samsung Galaxy S22 Ultra) |

Im Laufe der Jahre ist die Menge der Browser- und Geräteinformationen, die in der user-agent-Zeichenfolge enthalten sind, gestiegen.

## Anwendungsfälle für User-Agent

User-agents werden seit langem verwendet, um Marketing- und Entwicklungs-Teams wichtige Einblicke in die Anzeige von Website-Inhalten durch Browser, Betriebssysteme und Geräte sowie in die Interaktion zwischen Benutzern und Websites zu bieten. User-agents werden auch verwendet, um Spam zu blockieren und Bots zu filtern, die Sites aus verschiedenen Gründen durchsuchen.

Doch in den letzten Jahren nutzten manche Site-Eigentümer und Marketing-Anbieter den user-agent zusammen mit anderen in Anfrage-Headern enthaltenen Informationen, um digitale Fingerabdrücke zu erstellen, die zur Identifizierung von Benutzern ohne deren Wissen verwendet werden können. Trotz des wichtigen Zwecks, den der user-agent für Site-Eigentümer erfüllt, beschlossen Browser-Entwickler, Änderungen an der Funktionsweise von user-agents vorzunehmen, um potenzielle Datenschutzprobleme für Site-Besucher zu vermeiden.

Browser-Entwickler haben User-Agent Client Hints als Lösung für diese Herausforderung erstellt. Client Hints ermöglichen es Sites weiterhin, die erforderlichen Browser-, Betriebssystem- und Geräteinformationen zu erfassen, bieten aber gleichzeitig einen besseren Schutz vor verdeckten Tracking-Methoden wie dem Fingerabdruck.

## Client-Hinweise

User-Agent Client Hints bieten Website-Inhabern die Möglichkeit, auf einen Großteil der Informationen zuzugreifen, die im user-agent verfügbar sind, jedoch auf eine datenschutzfreundlichere Weise. Wenn moderne Browser einen user-agent verwenden, wird bei jeder Anfrage an den Webserver der gesamte user-agent gesendet, unabhängig davon, ob dies erforderlich ist. Client Hints hingegen zwingen den Server dazu, den Browser nach den zusätzlichen Informationen über den Client zu fragen. Nach Erhalt dieser Anfrage kann der Browser seine eigenen Richtlinien oder Benutzerkonfigurationen anwenden, um zu bestimmen, welche Daten zurückgegeben werden. Anstatt den gesamten user-agent standardmäßig für alle Anfragen verfügbar zu machen, wird der Zugriff jetzt eindeutig und überprüfbar verwaltet.

User-Agent Client Hints sind in Chrome seit Version 89 verfügbar. Aktuelle Versionen von Chromium-basierten Browsern wie Microsoft Edge, Opera, Brave, Chrome Android, Opera Android und Samsung Internet unterstützen ebenfalls die Client Hints-API.

Client Hints in den Headern der ersten vom Browser an einen Webserver gerichteten Anfrage enthalten die Browser-Marke, die Hauptversion des Browsers und einen Hinweis darauf, ob es sich bei dem Client um ein Mobilgerät handelt. Jedes Datenelement verfügt über einen eigenen Kopfzeilenwert, anstatt in einer einzelnen Benutzeragenten-Zeichenfolge zusammengefasst zu werden.

Im Folgenden finden Sie einige Client Hints:

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

…während dies der user-agent für denselben Browser ist:

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

Obwohl die Informationen ähnlich sind, enthält die erste Anfrage an den Server Client Hints, die nur eine Teilmenge der verfügbaren Elemente in der Zeichenfolge beinhalten. Bei der Anfrage fehlen die Betriebssystemarchitektur, die vollständige Betriebssystemversion, der Name der Layout-Engine, die Version der Layout-Engine und die vollständige Browser-Version. Bei nachfolgenden Anfragen ermöglicht die Client Hints-API Webservern jedoch, zusätzliche Details mit hoher Entropie (hohem Informationsgehalt) zum Gerät anzufordern. Wenn diese Werte mit hoher Entropie angefordert werden, kann die Browser-Antwort je nach der Browser-Richtlinie oder den Benutzereinstellungen diese Informationen enthalten.

Das folgende Beispiel ist ein JSON-Objekt, das von der Client Hints-API zurückgegeben wird, wenn Werte mit hoher Entropie angefordert werden:

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

Die Werte mit hoher Entropie beinhalten mehrere zusätzliche Informationen, die in den standardmäßigen Client Hints nicht verfügbar sind. Die folgende Tabelle enthält Informationen dazu, welche Daten in der Standardanfrage enthalten sind, verglichen mit den User-Agent Client Hints mit hoher Entropie.

| HTTP-Header | JavaScript | User-agent | Client-Hint | Client-Hint mit hoher Entropie |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | brands | Ja | Ja | Nein |
| Sec-CH-UA-Platform | Plattform | Ja | Ja | Nein |
| Sec-CH-UA-Mobile | mobile | Ja | Ja | Nein |
| Sec-CH-UA-Platform-Version | platformVersion | Ja | Nein | Ja |
| Sec-CH-UA-Arch | architecture | Ja | Nein | Ja |
| Sec-CH-UA-Model | model | Ja | Nein | Ja |
| Sec-CH-UA-Bitness | Bitness | Ja | Nein | Ja |
| Sec-CH-UA-Full-Version-List | fullVersionList | Ja | Nein | Ja |

## Migration Client Hints

Derzeit senden Chromium-basierte Browser in den Anfrage-Headern an Webserver weiterhin den user-agent gemeinsam mit Client Hints. Ab April 2022 bis Februar 2023 wird jedoch die Menge der in der user-agent-Zeichenfolge enthaltenen Daten reduziert. In anderen Browsern wie Safari und Firefox wird die user-agent-Zeichenfolge weiterhin verwendet. Aber auch sie werden den Umfang der darin enthaltenen Informationen verringern.

## Target-Anwendungsfälle, die Client-Hinweise erfordern

Die folgenden Anwendungsfälle in Target erfordern Client Hints:

### Zielgruppenattribute

Wenn Sie Target-Zielgruppen verwenden und eines der folgenden Zielgruppenattribute verwenden, erfordert Target, dass Client Hints die richtige Segmentierung durchführen:

* Browser
* Betriebssystem
* Mobile

### Profilskripte

Wenn Sie Profilskripte verwenden und das Attribut `user.browser` referenzieren (das auf den user-agent verweist), müssen Sie möglicherweise das Profilskript aktualisieren, um auch einen oder mehrere Client Hints zu überprüfen. Sie können auf jeden Client Hints über die Funktion `user.clientHint('sec-ch-ua-xxxxx')` zugreifen. Der Header-Name des Client-Hint muss vollständig in Kleinbuchstaben angegeben werden.

Das folgende Beispiel zeigt, wie ein Windows-Betriebssystem in einem Profilskript richtig erkannt wird:

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

Im Folgenden finden Sie eine Tabelle mit Client-Hinweisen und der entsprechenden Semantik für die Verwendung von Profilskripten.

| Client-Hint-Kopfzeile | Entropie | Zielgruppenattribut | Verwendung von Profilskripten |
| --- | --- | --- | --- |
| [Sek.-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | Niedrig | Browser | `user.clientHint('sec-ch-ua')` |
| [Sec-CH-UA-Arch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | Hoch | Benutzern über Profilskripte bereitgestellt werden | `user.clientHint('sec-ch-ua-arch')` |
| [Sek-CH-UA-Bitness](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | Hoch | Benutzern über Profilskripte bereitgestellt werden | `user.clientHint('sec-ch-ua-bitness')` |
| [Sec-CH-UA-Full-Version-List](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | Hoch | Browser | `user.clientHint('sec-ch-ua-full-version-list')` |
| [Sec-CH-UA-Mobile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | Niedrig | Mobile | `user.clientHint('sec-ch-ua-mobile')` |
| [Sec-CH-UA-Model](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | Hoch | Mobile | `user.clientHint('sec-ch-ua-model')` |
| [Sec-CH-UA-Platform](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | Niedrig | Betriebssystem | `user.clientHint('sec-ch-ua-platform')` |
| [Sec-CH-UA-Platform-Version](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | Hoch | Benutzern über Profilskripte bereitgestellt werden | `user.clientHint('sec-ch-ua-platform-version')` |

## Weitergeben von Client Hints an Adobe Target

In den folgenden Abschnitten finden Sie weitere Informationen darüber, wie Sie je nach Target-Implementierung Client Hints weitergeben.

### at.js-Version 2.9.0 (oder höher)

Ab at.js 2.9.0 werden User Agent Client Hints automatisch im Browser erfasst und an Target gesendet, wenn `getOffer/getOffers()` aufgerufen wird. Standardmäßig erfasst at.js nur Client Hints mit niedriger Entropie. Wenn Sie eine Zielgruppensegmentierung durchführen oder Profilskripte verwenden, die auf Daten basieren, die in den vorhergehenden Abschnitten als „Hohe Entropie“ bezeichnet wurden, müssen Sie at.js so konfigurieren, dass im Browser Client Hints mit „hoher Entropie“ über `targetGlobalSettings` erfasst werden.

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### Server-seitige SDKs

Weitere Informationen zum Übergeben von Client Hints über Server-seitige SDKs finden Sie unter [Client Hints](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints) unter Dokumentation zur Server-seitigen Implementierung.
