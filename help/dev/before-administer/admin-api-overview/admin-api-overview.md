---
title: Übersicht über die Adobe Target Admin-API
description: Überblick über die [!DNL Adobe Target Admin API]
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# Target Admin-API - Überblick

Dieser Artikel bietet einen Überblick über Hintergrundinformationen, die zum Verständnis und zur erfolgreichen Verwendung von [!DNL Adobe Target Admin API] erforderlich sind. Im folgenden Inhalt wird davon ausgegangen, dass Sie verstehen, wie [Authentifizierung konfigurieren](../configure-authentication.md) für [!DNL Adobe Target Admin API]s.

>[!NOTE]
>
>Wenn Sie [!DNL Target] über die Benutzeroberfläche verwalten möchten, lesen Sie den Abschnitt [Administration“ im *Handbuch für Adobe Target Business Practices*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=de).
>
>Die Admin-APIs und Profil-APIs werden häufig gemeinsam bezeichnet („Admin- und Profil-APIs„), können aber auch separat bezeichnet werden („Admin-APIs“ und „Profil-APIs„). Die Recommendations-API ist eine spezifische Implementierung einer [!DNL Target] Admin-API.

## Vorabinformationen 

Ersetzen Sie in allen Code-Beispielen für [Admin-](../../administer/admin-api/admin-api-overview-new.md)) {tenant} durch Ihren Mandantenwert, `your-bearer-token` durch das Zugriffstoken, das Sie mit Ihrem JWT generieren, und `your-api-key` durch Ihren API-Schlüssel aus der [Adobe Developer Console](https://developer.adobe.com/console/home). Weitere Informationen zu Mandanten und JWTs finden Sie im Artikel zum [&#x200B; der Authentifizierung für das Adobe [!DNL Target] Admin](../configure-authentication.md)APIs.

## Versionierung

Allen APIs ist eine Version zugeordnet. Es ist wichtig, die richtige Version der API bereitzustellen, die Sie verwenden möchten.

Wenn die Anfrage eine Payload enthält (POST oder PUT), wird die `Content-Type`-Kopfzeile der Anfrage verwendet, um die Version anzugeben.

Wenn die Anfrage keine Payload enthält (GET, DELETE oder OPTIONS), wird der `Accept`-Header verwendet, um die Version anzugeben.

Wenn keine Version bereitgestellt wird, wird für den Aufruf standardmäßig V1 (application/vnd.adobe.target.v1+json) verwendet.

>[!NOTE]
>
>Wenn die richtige Version nicht angegeben ist - z. B. wenn Sie eine V2-Payload verwenden, aber die Inhaltstyp-Kopfzeile nicht angeben -, antwortet die API mit einem nicht unterstützten Fehler, wenn die API nicht abwärtskompatibel ist.

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

Postman ist ein Programm, mit dem API-Aufrufe einfach ausgelöst werden können. Diese [Target-Admin-API-Postman](https://developers.adobetarget.com/api/#admin-postman-collection)Sammlung enthält alle Target-Admin-API-Aufrufe, für die eine Authentifizierung mithilfe von Aktivitäten, Audiences, Angeboten, Berichten, Mboxes und Umgebungen erforderlich ist

## Antwort-Codes

Im Folgenden finden Sie die allgemeinen Antwort-Codes für die Target Admin-APIs.

| Status | Beschreibung | Beschreibung |
| --- | --- | --- |
| 200 | [OK](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | OK |  |
| 400 | [Fehlerhafte Anfrage](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | Fehlerhafte Anfrage. Wahrscheinlich sind die in der Anfrage angegebenen Daten ungültig. |  |
| 401 | [Nicht autorisiert](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | Der Benutzer darf diesen Vorgang nicht ausführen. |  |
| 403 | [Verboten](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | Zugriff auf diese Ressource ist verboten. |  |
| 404 | [Nicht gefunden](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | Die referenzierte Ressource wurde nicht gefunden. |  |

## Aktivitäten

Eine Aktivität ermöglicht es Ihnen, Inhalte für Ihre Benutzerinnen und Benutzer zu testen oder zu personalisieren. Aktivitäten können einen der folgenden Typen aufweisen:

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=de)
* [Erlebnis-Targeting (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=de)
* [Recommendations](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html?lang=de)
* [Automatisierte Personalisierung](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=de)
* [Multivarianz-Test (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=de)

## Batch-Aktualisierungen

Mehrere Admin-APIs können als einzelne Batch-Anfrage ausgeführt werden.

### Ausführen von Aufrufen im Batch

`POST /{tenant}/target/batch`

Stapeln Sie mehrere API-Aufrufe zusammen und führen Sie sie in einem Batch aus.

Durch Batching können Sie Anweisungen für mehrere Vorgänge in einer einzigen HTTP-Anfrage übergeben. Sie können auch Abhängigkeiten zwischen verwandten Vorgängen angeben (siehe folgenden Abschnitt). TNT verarbeitet jeden Ihrer unabhängigen Vorgänge (möglicherweise parallel) und verarbeitet Ihre abhängigen Vorgänge sequenziell. Sobald alle Vorgänge abgeschlossen sind, wird eine konsolidierte Antwort zurückgegeben und die HTTP-Verbindung wird geschlossen.

Die Batch-API akzeptiert ein Array von logischen HTTP-Anfragen, die als JSON-Arrays dargestellt werden. Jede Anfrage hat eine -Methode (entspricht der HTTP-Methode GET/PUT/POST/DELETE usw.), eine relativeUrl (der Teil der URL nach admin/rest/), ein optionales Header-Array (entspricht HTTP-Headern) und einen optionalen Hauptteil (für POST- und PUT-Anfragen). Die Batch-API gibt ein Array von logischen HTTP-Antworten zurück, die als JSON-Arrays dargestellt werden. Jede Antwort hat einen Status-Code, ein optionales Headers-Array und einen optionalen Hauptteil (eine JSON-codierte Zeichenfolge). Um Batch-Anfragen durchzuführen, erstellen Sie ein JSON-Objekt, das jeden einzelnen auszuführenden Vorgang beschreibt. Die Anzahl der maximal zulässigen Vorgänge ist 256 (von 0 bis 255).

Angeben von Abhängigkeiten zwischen Vorgängen in der Anfrage Standardmäßig sind die in der Batch-API-Anfrage angegebenen Vorgänge unabhängig - sie können auf dem Server in beliebiger Reihenfolge ausgeführt werden, und ein Fehler in einem Vorgang wirkt sich nicht auf die Ausführung anderer Vorgänge aus.

Häufig sind die Vorgänge in der Anfrage abhängig - beispielsweise kann die Ausgabe eines Vorgangs in der Eingabe des nächsten Vorgangs verwendet werden. Beispielsweise muss das in operationId=0 erstellte Angebot in operationId=1 der Kampagnenerstellung verwendet werden.

Um zwei Batch-Vorgänge miteinander zu verknüpfen, geben Sie im abhängigen Vorgang die ID des erforderlichen Vorgangs an, z. B.: „dependsOnOperationId“ : 5. Auch IDs von Ressourcen, die über POST-Anfragen von Batch-Vorgängen erstellt wurden, können in abhängigen Vorgängen sowohl in „relativeUrl“ als auch in „body“ verwendet werden.

#### Berechtigungen und Einschränkungen

Um Batch-API-Aktionen ausführen zu können, muss der zugrunde liegende Benutzer über mindestens „Editor“-Rechte verfügen (für jeden einzelnen Vorgang, falls zusätzliche Rechte erforderlich sind als der Benutzer hat, schlägt der einzelne Vorgang fehl). Übliche Drosselungsstrategien werden auf Batch-API-Aktionen so angewendet, als ob jeder Vorgang einzeln ausgeführt worden wäre.

Die Batch-Verarbeitung ist abgeschlossen, wenn alle Vorgänge abgeschlossen sind. Ein Vorgang kann entweder erfolgreich (2xx StatusCode), fehlgeschlagen (4xx, 5xx Status-Code) oder übersprungen werden, da ein Abhängigkeitsvorgang fehlgeschlagen ist oder übersprungen wurde.

#### Anforderungsobjektparameter

| Attribut | Beschreibung | Beschränkungen | Standardeinstellung |
| --- | --- | --- | --- |
| Textkörper | Hauptteil für HTTP-Batch-Vorgang. wird für alle Aktionen außer POST und PUT ignoriert. kann auf IDs aus vorherigen Batch-Aktionen verweisen, z. B.: „offerId“: &quot;{operationIdResponse:0}&quot;, „segmentId“: &quot;{operationIdResponse:1}&quot; | muss eine gültige JSON sein. Im Fall des Verweises auf eine operationIdResponse sollte die verweisende operationId-Antwort eine gültige ID sein und die Methode für diese Aktion sollte POST sein | Leere {} |  |
| dependsOnOperationIds | Liste der Einschränkungs-IDs, die sicherstellen, dass der aktuelle Vorgang nur ausgeführt wird, wenn die angegebenen Vorgänge erfolgreich abgeschlossen wurden. Kann verwendet werden, um eine Verkettung von Vorgängen zu erzielen. | Es sind maximal 255 Vorgänge zulässig; eindeutige Werte sind nur zulässig; sollten auf eine gültige operationId im Array verweisen; zyklische Abhängigkeiten sind nicht zulässig |  |  |
| Kopfzeilen | Array von Schlüssel-Wert-Headern, die mit einem bestimmten Vorgang gesendet werden sollen. Wenn die Authentifizierung für die Batch-API über die Autorisierungskopfzeile durchgeführt wurde, wird sie auch für einzelne Vorgänge kopiert. | Maximal zulässige Anzahl von Kopfzeilen im Array ist 50 | Content-Type: application/json |  |
| header->name | Header-Name | sollte unter anderen Kopfzeilennamen eindeutig sein. Bei Kopfzeilen wird von RFC nicht zwischen Groß- und Kleinschreibung unterschieden. Andernfalls überschreiben sich die Werte gegenseitig. |  |  |
| headers->value | Kopfzeilenwert | K. A. | Leere Zeichenfolge |  |
| method | Zu verwendende HTTP-Methode. Verfügbare Optionen: GET, POST, PUT, PATCH, DELETE | Nur GET-, POST-, PUT-, PATCH- und DELETE-Methoden sind zulässig |  |  |
| operationId | Vorgangs-ID, die verwendet wird, um einen Vorgang neben anderen Vorgängen für Antworten und Verweise auf Ergebnisse zu identifizieren. | Eindeutig unter anderen Vorgängen; Werte von 0-255 |  |  |
| Betrieb | Liste der im Batch auszuführenden Vorgänge. Reihenfolge ist nicht relevant. | Es sind maximal 256 Vorgänge zulässig |  |  |
| relativeUrl | relative URL für die Admin-REST-API, der Teil nach &quot;/admin/rest/&quot;. Kann Abfragezeichenfolgenparameter enthalten wie: &quot;/v2/campaigns?limit=10&amp;offset=10“. kann auf URLs verweisen, die IDs aus vorherigen Batch-Aktionen enthalten, z. B.: &quot;/v1/offers/{operationIdResponse:0}&quot;. Wenn Abfrageparameter gesendet werden, müssen sie URL-kodiert sein. | sollte mit / (relativ sein) beginnen; nur neue gültige JSON-APIs werden unterstützt; im Fall einer ungültigen relativen URL wird eine 404-Antwort für einen bestimmten Vorgang zurückgegeben. Im Fall des Verweises auf eine operationIdResponse sollte die verweisende operationId-Antwort eine gültige ID sein und die Methode für diese Aktion sollte POST sein |  |  |

#### Beispielobjekt für die Anfrage

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

#### Parameter des Antwortobjekts

| Parameter | Beschreibung |
| --- | --- |
| operationId | Vorgangs-ID, die verwendet wird, um einen Vorgang neben anderen Vorgängen zu identifizieren, und dieselbe ID, die in der POST-Anfrage gesendet wurde. |  |
| übersprungen | BOOLEN-Markierung, um zu markieren, ob der Vorgang ausgeführt oder übersprungen wurde. Ist „true“, wenn der aktuelle Vorgang von einem fehlgeschlagenen Vorgang abhängt (gibt einen StatusCode-Wert zurück, der von 2xx abweicht). |  |
| statusCode | zurückgegeben, werden alle abhängigen Vorgänge übersprungen (nicht ausgeführt). |  |
| Kopfzeilen | Array von Schlüssel-Wert-Headern, die als Antwort für einen bestimmten Vorgang gesendet werden sollen. |  |
| header->name | Header-Name |  |
| headers->value | Kopfzeilenwert |  |
| Textkörper | Hauptteil für HTTP-Batch-Antwortvorgang |  |

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
