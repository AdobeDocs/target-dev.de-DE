---
title: Adobe Target-Bereitstellungs-API zur Identifizierung von Besuchern
description: Wie kann ich Benutzer in [!DNL Adobe Target] identifizieren?
keywords: Versandschnittstelle
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 7%

---

# Identifizieren von Besuchern

Es gibt mehrere Möglichkeiten, einen Besucher innerhalb von [!DNL Adobe Target] zu identifizieren.

Target verwendet drei Kennungen:

| Feldname | Beschreibung |
| --- | --- |
| `tntId` | Der `tntId` ist die primäre Kennung in [!DNL Target] für einen Benutzer. Sie können diese ID angeben oder [!DNL Target] generiert sie automatisch, wenn die Anforderung keine enthält. |
| `thirdPartyId` | Der `thirdPartyId` ist die Kennung Ihres Unternehmens für den Benutzer, den Sie bei jedem Aufruf senden können. Wenn sich ein Benutzer bei der Site eines Unternehmens anmeldet, erstellt das Unternehmen in der Regel eine ID, die an das Konto, die Treuekarte, die Mitgliedsnummer oder andere für dieses Unternehmen gültige Kennungen des Besuchers gebunden ist. |
| `marketingCloudVisitorId` | Der `marketingCloudVisitorId` wird verwendet, um Daten zwischen verschiedenen Adobe-Lösungen zusammenzuführen und freizugeben. Der `marketingCloudVisitorId` ist für Integrationen mit Adobe Analytics und Adobe Audience Manager erforderlich. |
| `customerIds` | Neben der Experience Cloud-Besucher-ID können zusätzliche [Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) und ein authentifizierter Status für jeden Besucher verwendet werden. |

## [!DNL Target] ID

Die [!DNL Target] ID oder `tntId` kann als Geräte-ID betrachtet werden. Diese `tntId` wird automatisch von [!DNL Target] generiert, wenn sie nicht in der Anfrage angegeben ist. Anschließend müssen nachfolgende Anfragen diesen Wert `tntId` enthalten, damit der richtige Inhalt an ein vom Benutzer verwendetes Gerät gesendet werden kann.

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

Der obige Beispielaufruf zeigt, dass ein `tntId` nicht übergeben werden muss. In diesem Szenario generiert [!DNL Target] einen `tntId` und stellt ihn in der Antwort bereit, wie hier gezeigt:

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

Die generierte `tntId` ist `10abf6304b2714215b1fd39a870f01afc.28_20`. Beachten Sie, dass `tntId` verwendet werden muss, wenn [!UICONTROL Adobe Target Delivery API] für denselben Benutzer sitzungsübergreifend aufgerufen wird.

## Marketing Cloud-Besucher-ID

Der `marketingCloudVisitorId` ist eine universelle und beständige ID, mit der Ihre Besucher lösungsübergreifend in der Experience Cloud identifiziert werden. Wenn Ihr Unternehmen den ID-Dienst implementiert, können Sie mit dieser ID denselben Site-Besucher und dessen Daten in verschiedenen Experience Cloud-Lösungen wie Adobe Target, Adobe Analytics oder Adobe Audience Manager identifizieren. Beachten Sie, dass der `marketingCloudVisitorId` erforderlich ist, wenn Sie Analytics und Audience Manager nutzen und in diese integrieren.

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

Der obige Beispielaufruf zeigt, wie eine `marketingCloudVisitorId`, die vom Experience Cloud ID-Dienst abgerufen wurde, an Adobe Target übergeben wird. In diesem Szenario generiert [!DNL Target] einen `tntId` , da er nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `marketingCloudVisitorId` zugeordnet wird, wie in der Antwort unten dargestellt.

## Drittanbieter-ID

Wenn Ihr Unternehmen zur Identifizierung Ihres Besuchers eine ID verwendet, können Sie mit `thirdPartyID` Inhalte bereitstellen. Sie müssen jedoch für jeden [!UICONTROL Adobe Target Delivery API] -Aufruf den Wert `thirdPartyID` angeben.

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

Der obige Beispielaufruf zeigt einen &quot;`thirdPartyId`&quot;, eine beständige ID, die Ihr Unternehmen zur Identifizierung eines Endbenutzers verwendet, unabhängig davon, ob er über Web-, mobile oder IoT-Kanäle mit Ihrem Unternehmen interagiert. Mit anderen Worten, die `thirdPartyId` verweisen auf Benutzerprofildaten, die kanalübergreifend verwendet werden können. In diesem Szenario generiert [!DNL Target] einen `tntId`, da er nicht an den ursprünglichen Aufruf übergeben wurde, der dem bereitgestellten `thirdPartyId` zugeordnet wird, wie in der Antwort unten dargestellt.

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

[Kunden-IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) können hinzugefügt und mit einer Experience Cloud-Besucher-ID verknüpft werden. Beim Senden von `customerIds` muss auch der `marketingCloudVisitorId` angegeben werden. Außerdem kann für jeden Besucher ein Authentifizierungsstatus mit jedem `customerId` angegeben werden. Der folgende Authentifizierungsstatus kann berücksichtigt werden:

| Authentifizierungsstatus | Benutzerstatus |
| --- | --- |
| `unknown` | Unbekannt oder nie authentifiziert. Dieser Status kann für Szenarien wie einen Besucher verwendet werden, der auf Ihre Site gelangt ist, indem er auf eine Display-Anzeige klickt. |
| `authenticated` | Der Benutzer ist zurzeit in einer aktiven Sitzung auf Ihrer Website oder in Ihrer Applikation authentifiziert. |
| `logged_out` | Der Benutzer war authentifiziert, hat sich dann aber aktiv abgemeldet. Der authentifizierte Status wurde absichtlich beendet. Der Benutzer möchte nicht mehr als authentifiziert behandelt werden. |

Beachten Sie, dass Target nur dann auf die Benutzerprofildaten verweist, die gespeichert und mit der Kunden-ID verknüpft sind, wenn die Kunden-ID den Status &quot;`authenticated`&quot; aufweist. Wenn die Kunden-ID den Status `unknown` oder `logged_out` aufweist, wird die Kunden-ID ignoriert und alle damit verbundenen Benutzerprofildaten werden nicht für Zielgruppen-Targeting verwendet.

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

Der obige Beispielaufruf zeigt, wie eine `customerId` mit einer `authenticatedState` gesendet wird. Beim Senden einer `customerId` sind die `integrationCode`, `id` und `authenticatedState` sowie die `marketingCloudVisitorId` erforderlich. Die `integrationCode` ist der Alias der [Kundenattributdatei](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=de), die Sie über CRS bereitgestellt haben.

## Zusammengeführtes Profil

Sie können `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anforderung kombinieren. In diesem Szenario pflegt Adobe Target die Zuordnung all dieser IDs und veröffentlicht sie an einen Besucher. Erfahren Sie, wie Profile mit den verschiedenen Kennungen [zusammengeführt und in Echtzeit synchronisiert werden](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html).

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

Der obige Beispielaufruf zeigt, wie Sie `tntId`, `thirdPartyID` und `marketingCloudVisitorId` in derselben Anforderung kombinieren können. Alle drei IDs werden auch in der Antwort zurückgegeben.
