---
title: Übersicht über die Adobe Target Admin-API
description: Übersicht über die [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 3%

---

# Target Admin-API - Übersicht

Dieser Artikel bietet einen Überblick über Hintergrundinformationen, die zum Verständnis und zur Verwendung von [!DNL Adobe Target Admin API]erfolgreich ist. Im folgenden Inhalt wird davon ausgegangen, dass Sie wissen, wie [Authentifizierung konfigurieren](../configure-authentication.md) für [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Wenn Sie [!DNL Target] über die Benutzeroberfläche sehen Sie die [Abschnitt *Handbuch für Adobe Target Business Practices*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).
>
>Die Admin-APIs und Profil-APIs werden häufig kollektiv bezeichnet (&quot;Admin- und Profil-APIs&quot;), können aber auch separat referenziert werden (&quot;Admin-APIs&quot;und &quot;Profil-APIs&quot;). Die Recommendations-API ist eine spezifische Implementierung einer [!DNL Target] Admin-API.

## Vorabinformationen 

In allen Codebeispielen für [Admin-APIs](../../administer/admin-api/admin-api-overview-new.md), ersetzen {tenant} mit Ihrem Mandantenwert, `your-bearer-token` mit dem Zugriffstoken, das Sie mit Ihrem JWT generieren, und `your-api-key` mit Ihrem API-Schlüssel aus der [Adobe Developer-Konsole](https://developer.adobe.com/console/home). Weitere Informationen zu Mandanten und JWTs finden Sie im Artikel zum [Authentifizierung konfigurieren](../configure-authentication.md) für Adobe [!DNL Target] Admin-APIs.

## Versionierung

Alle APIs verfügen über eine zugehörige Version. Es ist wichtig, die richtige Version der API bereitzustellen, die Sie verwenden möchten.

Wenn die Anfrage eine Payload enthält (POST oder PUT), wird die `Content-Type` -Kopfzeile der Anfrage wird verwendet, um die Version anzugeben.

Wenn die Anfrage keine Payload enthält (GET, DELETE oder OPTIONS), wird die `Accept` -Kopfzeile wird verwendet, um die Version anzugeben.

Wenn keine Version bereitgestellt wird, wird für den Aufruf standardmäßig V1 (application/vnd.adobe.target.v1+json) verwendet.

>[!NOTE]
>
>Wenn die richtige Version nicht angegeben ist (z. B. wenn Sie eine V2-Payload verwenden, aber die Content-Type-Kopfzeile nicht angeben), antwortet die API mit einem nicht unterstützten Fehler, wenn die API nicht abwärtskompatibel ist.

Fehlermeldung für nicht unterstützte Funktionen

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

Admin Postman-Sammlung

Postman ist eine Anwendung, die das Auslösen von API-Aufrufen erleichtert. Diese [Postman-Sammlung für Target-Admin-API](https://developers.adobetarget.com/api/#admin-postman-collection) enthält alle Target Admin-API-Aufrufe, für die eine Authentifizierung mithilfe von Aktivitäten, Zielgruppen, Angeboten, Berichten, Mboxes und Umgebungen erforderlich ist

## Antwortcodes

Hier finden Sie die gebräuchlichen Antwort-Codes für die Target Admin-APIs.

| Status | Beschreibung | Beschreibung |
| --- | --- | --- |
| 200 | [OK](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) |  OK- |  |
| 400 | [Unzulässige Anfrage](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Unzulässige Anfrage. Wahrscheinlich sind die in der Anfrage angegebenen Daten ungültig. |  |
| 401 | [Nicht aktualisieren](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | Der Benutzer darf diesen Vorgang nicht ausführen. |  |
| 403 | [Nicht erlaubt](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | Der Zugriff auf diese Ressource ist verboten. |  |
| 404 | [nicht gefunden](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | Die referenzierte Ressource wurde nicht gefunden. |  |

## Aktivitäten

Mit einer Aktivität können Sie Inhalte für Ihre Benutzer testen oder personalisieren. Aktivitäten können einen der folgenden Typen aufweisen:

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Erlebnis-Targeting (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Automatisierte Personalisierung](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivariate Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## Batch-Aktualisierungen

Mehrere Admin-APIs können als eine Batch-Anfrage ausgeführt werden.

### Ausführen von Aufrufen im Batch-Modus

`POST /{tenant}/target/batch`

Stapeln Sie mehrere API-Aufrufe zusammen und führen Sie sie in einem Batch aus.

Mit der Stapelverarbeitung können Sie Anweisungen für mehrere Vorgänge in einer einzelnen HTTP-Anforderung übergeben. Sie können auch Abhängigkeiten zwischen verwandten Vorgängen angeben (siehe Abschnitt unten). TNT verarbeitet jeden Ihrer unabhängigen Vorgänge (möglicherweise parallel) und verarbeitet Ihre abhängigen Vorgänge sequenziell. Sobald alle Vorgänge abgeschlossen sind, wird eine konsolidierte Antwort zurückgegeben und die HTTP-Verbindung wird geschlossen.

Die Batch-API akzeptiert ein Array von logischen HTTP-Anfragen, die als JSON-Arrays dargestellt werden. Jede Anfrage verfügt über eine -Methode (entspricht der HTTP-Methode GET/PUT/POST/DELETE usw.), eine relativeUrl (der Teil der URL nach Admin/Rest/), ein optionales Header-Array (entspricht HTTP-Headern) und einen optionalen Text (für POST- und PUT-Anfragen). Die Batch-API gibt ein Array logischer HTTP-Antworten zurück, die als JSON-Arrays dargestellt werden. Jede Antwort hat einen Statuscode, ein optionales Header-Array und einen optionalen Hauptteil (eine JSON-kodierte Zeichenfolge). Erstellen Sie für gebündelte Anfragen ein JSON-Objekt, das die einzelnen auszuführenden Vorgänge beschreibt. Die Anzahl der maximal zulässigen Vorgänge beträgt 256 (von 0 bis 255).

Angeben von Abhängigkeiten zwischen Vorgängen in der Anfrage Standardmäßig sind die in der Batch-API-Anfrage angegebenen Vorgänge unabhängig. Sie können auf dem Server in beliebiger Reihenfolge ausgeführt werden und ein Fehler in einem Vorgang wirkt sich nicht auf die Ausführung anderer Vorgänge aus.

Oft sind die Vorgänge in der Anfrage abhängig - beispielsweise kann die Ausgabe eines Vorgangs in der Eingabe des nächsten Vorgangs verwendet werden. Beispielsweise muss ein in operationId=0 erstelltes Angebot in der Kampagnenerstellung operationId=1 verwendet werden.

Um zwei Batch-Vorgänge miteinander zu verknüpfen, geben Sie im abhängigen Vorgang die ID des erforderlichen Vorgangs an, z. B. &quot;dependsOnOperationId&quot; : 5. Auch IDs von erstellten Ressourcen über POST-Anfragen von Batch-Vorgängen können in abhängigen Vorgängen sowohl in &quot;relativeUrl&quot;als auch in &quot;body&quot;verwendet werden.

#### Berechtigungen und Einschränkungen

Um Batch-API-Aktionen ausführen zu können, muss der zugrunde liegende Benutzer mindestens &quot;Editor&quot;-Rechte haben (für jeden einzelnen Vorgang sind zusätzliche Rechte erforderlich, als der Benutzer dies hat). Übliche Drosselungsstrategien werden auf Batch-API-Aktionen angewendet, als ob jeder Vorgang einzeln ausgeführt wurde.

Die Stapelverarbeitung wird abgeschlossen, wenn alle Vorgänge abgeschlossen wurden. Ein Vorgang kann entweder erfolgreich (2xx statusCode), fehlgeschlagen (4xx, 5xx-Statuscode) oder übersprungen sein, da ein Abhängigkeitsvorgang fehlgeschlagen ist oder übersprungen wurde.

#### Objekt-Parameter anfordern

| Attribut | Beschreibung | Beschränkungen | Standardeinstellung |
| --- | --- | --- | --- |
| body | body für HTTP-Batch-Vorgang. wird für alle Aktionen außer POST und PUT ignoriert. kann auf IDs aus vorherigen Batch-Aktionen verweisen, z. B.: &quot;offerId&quot;: &quot;{operationIdResponse:0}&quot;, &quot;segmentId&quot;: &quot;{operationIdResponse:1}&quot; | sollte eine gültige JSON sein. Wenn auf eine operationIdResponse verwiesen wird, sollte die referenzierte operationId-Antwort eine gültige ID sein und die Methode für diese Aktion sollte POST sein. | leeres Objekt {} |  |
| dependsOnOperationIds | Liste der Einschränkungs-IDs, die sicherstellen, dass der aktuelle Vorgang nur ausgeführt wird, wenn die angegebenen Vorgänge erfolgreich abgeschlossen wurden. Kann verwendet werden, um eine Verkettung von Vorgängen zu erreichen. | maximal 255 Vorgänge sind zulässig; eindeutige Werte sind nur zulässig; sollten auf eine gültige operationId im Array verweisen; zyklische Abhängigkeiten sind nicht zulässig |  |  |
| Kopfzeilen | Array von Schlüssel-Wert-Headern, die mit einem bestimmten Vorgang gesendet werden. Wenn die Authentifizierung für die Batch-API über die Autorisierungs-Kopfzeile durchgeführt wurde, wird sie auch für einzelne Vorgänge kopiert. | Maximale Anzahl von Headern im erlaubten Array ist 50 | Content-Type: application/json |  |
| headers->name | Headername | sollte unter anderen Kopfzeilennamen eindeutig sein. Bei den Headern wird von rfc nicht zwischen Groß- und Kleinschreibung unterschieden. Andernfalls werden sich die Werte überschreiben. |  |  |
| headers->value | Kopfzeilenwert | K. A. | leere Zeichenfolge |  |
| method | HTTP-Methode. Verfügbare Optionen: GET, POST, PUT, PATCH, DELETE | Nur GET, POST, PUT, PATCH, DELETE-Methoden sind zulässig |  |  |
| operationId | Vorgangskennung, die zur Identifizierung eines Vorgangs unter anderen Vorgängen für Antworten und referenzierende Ergebnisse verwendet wird. | einzigartig unter anderen Vorgängen; Werte von 0-255 |  |  |
| Vorgänge | Liste der in einem Batch auszuführenden Vorgänge. Bestellung ist nicht relevant. | maximal 256 Vorgänge zulässig sind |  |  |
| relativeUrl | relative URL für die Admin Rest-API, der Teil nach &quot;/admin/rest/&quot;. Kann Abfragezeichenfolgenparameter wie &quot;/v2/campaigns?limit=10&amp;offset=10&quot;enthalten. kann auf URLs verweisen, die IDs aus vorherigen Batch-Aktionen enthalten, z. B. &quot;/v1/offer/{operationIdResponse:0}&quot;. Wenn Abfrageparameter gesendet werden, müssen sie URL-kodiert sein. | sollte mit / beginnen (relativ sein); es werden nur neue gültige JSON-APIs unterstützt. Bei ungültiger relativeURL wird eine 404-Antwort für einen bestimmten Vorgang zurückgegeben. Wenn auf eine operationIdResponse verwiesen wird, sollte die referenzierte operationId-Antwort eine gültige ID sein und die Methode für diese Aktion sollte POST sein. |  |  |

#### Beispielanfrageobjekt

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### Antwortobjektparameter

| Parameter | Beschreibung |
| --- | --- |
| operationId | Vorgangskennung, die zur Identifizierung eines Vorgangs unter anderen Vorgängen verwendet wird, die gleiche ID wie die in der POST-Anfrage gesendete. |  |
| übersprungen | boolen Markierung, um zu kennzeichnen, ob der Vorgang ausgeführt oder übersprungen wurde. Ist &quot;true&quot;, wenn der aktuelle Vorgang von einem fehlgeschlagenen Vorgang abhängt (der einen statusCode -Wert zurückgegeben hat, der sich von 2xx unterscheidet). |  |
| statusCode | zurückgegeben, werden alle abhängigen Vorgänge übersprungen (nicht ausgeführt). |  |
| Kopfzeilen | Array von Schlüssel-Wert-Headern, die als Antwort für einen bestimmten Vorgang gesendet werden. |  |
| headers->name | Headername |  |
| headers->value | Kopfzeilenwert |  |
| body | body für HTTP-Batch-Antwortvorgang |  |

#### Beispielantwortobjekt

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
