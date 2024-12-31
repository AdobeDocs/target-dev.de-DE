---
title: Adobe Target-Bereitstellungs-API zur Besucheridentifizierung
description: Wie kann ich einen Benutzer in identifizieren [!DNL Adobe Target]?
keywords: Bereitstellungs-API
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 7%

---

# Identifizieren von Besuchern

Es gibt mehrere Möglichkeiten, einen Besucher in [!DNL Adobe Target] zu identifizieren.

Target verwendet drei Kennungen:

| Feldname | Beschreibung |
| --- | --- |
| `tntId` | Der `tntId` ist die primäre Kennung in [!DNL Target] für einen Benutzer. Sie können diese ID angeben oder [!DNL Target] generiert sie automatisch, wenn die Anfrage keine enthält. |
| `thirdPartyId` | Die `thirdPartyId` ist die Kennung Ihres Unternehmens für den Benutzer, die Sie mit jedem Aufruf senden können. Wenn sich ein(e) Benutzende(r) auf der Website eines Unternehmens anmeldet, erstellt das Unternehmen normalerweise eine ID, die mit dem Konto, der Treuekarte, der Mitgliedschaftsnummer oder anderen Kennungen des/der Besuchenden für dieses Unternehmen verknüpft ist. |
| `marketingCloudVisitorId` | Die `marketingCloudVisitorId` wird verwendet, um Daten zwischen verschiedenen Adobe-Lösungen zusammenzuführen und freizugeben. Die `marketingCloudVisitorId` ist für Integrationen mit Adobe Analytics und Adobe Audience Manager erforderlich. |
| `customerIds` | Neben der Experience Cloud-Besucher-ID können zusätzliche [Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) und ein Authentifizierungsstatus für jeden Besucher verwendet werden. |

## [!DNL Target] ID

Die [!DNL Target]-ID oder der `tntId` kann als Geräte-ID angezeigt werden. Diese `tntId` wird automatisch von [!DNL Target] generiert, wenn sie nicht in der Anfrage angegeben wird. Danach müssen nachfolgende Anfragen diese `tntId` enthalten, damit der richtige Inhalt an ein Gerät gesendet werden kann, das vom Benutzer verwendet wird.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
  "context": {
    "channel": "web",
    "browser" : {
      "host" : "demo"
    },
    "address" : {
      "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
    },
    "screen" : {
      "width" : 1200,
      "height": 1400
    }
  },
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

Der obige Beispielaufruf zeigt, dass kein `tntId` übergeben werden muss. In diesem Szenario generiert [!DNL Target] eine `tntId` und stellt sie in der Antwort bereit, wie hier gezeigt:

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

Der generierte `tntId` ist `10abf6304b2714215b1fd39a870f01afc.28_20`. Beachten Sie, dass diese `tntId` verwendet werden muss, wenn der [!UICONTROL Adobe Target Delivery API] sitzungsübergreifend für denselben Benutzer aufgerufen wird.

## Marketing Cloud-Besucher-ID

Die `marketingCloudVisitorId` ist eine universelle und persistente ID, die Ihre Besuchenden über alle Lösungen hinweg auf der Experience Cloud identifiziert. Wenn Ihr Unternehmen den ID-Service implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in verschiedenen Experience Cloud-Lösungen wie Adobe Target, Adobe Analytics oder Adobe Audience Manager identifizieren. Beachten Sie, dass die `marketingCloudVisitorId` bei der Nutzung und Integration mit Analytics und Audience Manager erforderlich ist.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
  },
  "context": {
    "channel": "web",
    "browser" : {
      "host" : "demo"
    },
    "address" : {
      "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
    },
    "screen" : {
      "width" : 1200,
      "height": 1400
    }
  },
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

Der obige Beispielaufruf zeigt, wie ein `marketingCloudVisitorId`, das vom Experience Cloud-ID-Service abgerufen wurde, an Adobe Target übergeben wird. In diesem Szenario generiert [!DNL Target] eine `tntId`, da sie nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `marketingCloudVisitorId` zugeordnet wird, wie in der Antwort unten dargestellt.

## Drittanbieter-ID

Wenn Ihr Unternehmen eine ID verwendet, um Ihren Besucher zu identifizieren, können Sie `thirdPartyID` verwenden, um Inhalte bereitzustellen. Sie müssen jedoch die `thirdPartyID` für jeden [!UICONTROL Adobe Target Delivery API]-Aufruf angeben.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
  },
  "context": {
    "channel": "web",
    "browser" : {
      "host" : "demo"
    },
    "address" : {
      "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
    },
    "screen" : {
      "width" : 1200,
      "height": 1400
    }
  },
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

Der obige Beispielaufruf zeigt eine `thirdPartyId`. Dies ist eine persistente ID, die Ihr Unternehmen verwendet, um einen Endbenutzer zu identifizieren, unabhängig davon, ob er über Web-, Mobil- oder IoT-Kanäle mit Ihrem Unternehmen interagiert. Mit anderen Worten, die `thirdPartyId` verweist auf Benutzerprofildaten, die kanalübergreifend verwendet werden können. In diesem Szenario generiert [!DNL Target] eine `tntId`, da sie nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `thirdPartyId` zugeordnet wird, wie in der Antwort unten dargestellt.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) können hinzugefügt und mit einer Experience Cloud-Besucher-ID verknüpft werden. Bei Versand `customerIds` muss auch die `marketingCloudVisitorId` angegeben werden. Darüber hinaus kann für jeden Besucher ein Authentifizierungsstatus zusammen mit jedem `customerId` angegeben werden. Der folgende Authentifizierungsstatus kann berücksichtigt werden:

| Authentifizierungsstatus | Benutzerstatus |
| --- | --- |
| `unknown` | Unbekannt oder nie authentifiziert. Dieser Status kann für Szenarien wie einen Besucher verwendet werden, der auf Ihrer Site gelandet ist, indem er auf eine Display-Anzeige klickt. |
| `authenticated` | Der Benutzer ist zurzeit in einer aktiven Sitzung auf Ihrer Website oder in Ihrer Applikation authentifiziert. |
| `logged_out` | Der Benutzer war authentifiziert, hat sich dann aber aktiv abgemeldet. Der authentifizierte Status wurde absichtlich beendet. Der Benutzer möchte nicht mehr als authentifiziert behandelt werden. |

Beachten Sie, dass Target nur dann auf die Benutzerprofildaten verweist, wenn sich die Kunden-ID in `authenticated` Zustand befindet und mit der Kunden-ID verknüpft ist. Wenn sich die Kunden-ID im `unknown` oder `logged_out` Status befindet, wird die Kunden-ID ignoriert, und alle Benutzerprofildaten, die mit ihr verknüpft sind, werden nicht für das Audience-Targeting genutzt.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
      "id": {
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

Der obige Beispielaufruf zeigt, wie ein `customerId` mit einem `authenticatedState` gesendet wird. Beim Senden eines `customerId` sind die `integrationCode`, `id` und `authenticatedState` sowie die `marketingCloudVisitorId` erforderlich. Der `integrationCode` ist der Alias der [Kundenattributdatei), ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=de) Sie über CRS bereitgestellt haben.

## Zusammengeführtes Profil

Sie können `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anfrage kombinieren. In diesem Szenario verwaltet Adobe Target die Zuordnung all dieser IDs und heftet sie an einen Besucher an. Erfahren Sie, wie Profile mithilfe [ verschiedenen Kennungen in Echtzeit zusammengeführt ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) synchronisiert werden.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
      "id": {
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

Der obige Beispielaufruf zeigt, wie Sie `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anfrage kombinieren können. Alle drei IDs werden ebenfalls in der Antwort zurückgegeben.
