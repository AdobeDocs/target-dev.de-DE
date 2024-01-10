---
title: Adobe Target Bulk-Profil-Update-API
description: Verwendung von [!DNL Adobe Target] [!UICONTROL Bulk-Profil-Update-API] zum Senden mehrerer Besucherprofildaten an [!DNL Target] zur Verwendung beim Targeting.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: 3d90616b0a920abea380d4cfcd1227eafde86adb
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

Die [!DNL Adobe Target] [!UICONTROL Bulk-Profil-Update-API] ermöglicht Ihnen, mithilfe einer Batch-Datei Benutzerprofile für mehrere Besucher einer Website stapelweise zu aktualisieren.

Verwenden der [!UICONTROL Bulk-Profil-Update-API]können Sie detaillierte Besucherprofildaten in Form von Profilparametern für viele Benutzer an senden. [!DNL Target] aus einer beliebigen externen Quelle. Externe Quellen können beispielsweise CRM-Systeme (Customer Relationship Management) oder POS-Systeme (Point of Sale) sein, die normalerweise nicht auf einer Webseite verfügbar sind.

| Version  | URL-Beispiel | Funktionen |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Nur Unterstützung für Massenaktualisierung von Profilen. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Erstellen Sie ein Profil, falls nicht gefunden.</li><li>Aktualisierung des Zeilenstatus.</li></ul> |

>[!NOTE]
>
>Version 2 (v2) der [!UICONTROL Bulk-Profil-Update-API] ist die aktuelle Version. Allerdings [!DNL Target] unterstützt weiterhin Version 1 (v1).

## Vorteile der Bulk-Profil-Update-API

* Keine Begrenzung der Anzahl der Profilattribute.
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen

* Die Batch-Datei muss kleiner als 50 MB sein. Außerdem sollte die Gesamtzeilenzahl 500.000 Zeilen pro Upload nicht überschreiten.
* Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.
* Die Anzahl der Zeilen, die Sie über einen Zeitraum von 24 Stunden in nachfolgenden Batches hochladen können, ist nicht beschränkt. Allerdings kann der Importverlauf während der Geschäftszeiten gedrosselt werden, um sicherzustellen, dass andere Prozesse effizient ablaufen.
* Aufeinander folgende v2-Batch-Aktualisierungsaufrufe ohne dazwischen liegende Mbox-Aufrufe für dieselben thirdPartyIds überschreiben die Eigenschaften, die im ersten Batch-Aktualisierungsaufruf aktualisiert wurden.
* [!DNL Adobe] garantiert nicht, dass 100 % der Batch-Profildaten in Target integriert und beibehalten werden und daher für die Verwendung beim Targeting verfügbar sind. Beim aktuellen Design besteht die Möglichkeit, dass ein kleiner Anteil der Daten (bis zu 0,1 % der großen Produktions-Batches) nicht integriert oder beibehalten wird.

## Batch-Datei

Um Profildaten stapelweise zu aktualisieren, erstellen Sie eine Batch-Datei. Die Batch-Datei ist eine Textdatei mit durch Kommas getrennten Werten, die der folgenden Beispieldatei ähneln.

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

Sie verweisen auf diese Datei im POST-Aufruf an [!DNL Target] -Server zur Verarbeitung der Datei. Beachten Sie beim Erstellen der Batch-Datei Folgendes:

* In der ersten Zeile der Datei müssen Spaltenüberschriften angegeben werden.
* Die erste Kopfzeile sollte entweder eine `pcId` oder `thirdPartyId`. Die [!UICONTROL Marketing Cloud-Besucher-ID] wird nicht unterstützt. [!UICONTROL pcId] ist [!DNL Target]-generierte visitorID. `thirdPartyId` ist eine von der Clientanwendung angegebene ID, die an [!DNL Target] durch einen Mbox-Aufruf als `mbox3rdPartyId`. Es muss hier als `thirdPartyId`.
* Die in der Batch-Datei angegebenen Parameter und Werte müssen aus Sicherheitsgründen mit UTF-8 URL-kodiert werden. Parameter und Werte können zur Verarbeitung über HTTP-Anforderungen an andere Edge-Knoten weitergeleitet werden.
* Die Parameter müssen im Format `paramName` nur. Die Parameter werden in [!DNL Target] as `profile.paramName`.
* Wenn Sie [!UICONTROL Bulk-Profil-Update-API] v2: Sie müssen nicht alle Parameterwerte für jede `pcId`. Profile werden für alle `pcId` oder `mbox3rdPartyId` das nicht in [!DNL Target]. Wenn Sie v1 verwenden, werden Profile nicht für fehlende pcIds oder mbox3rdPartyIds erstellt.
* Die Batch-Datei muss kleiner als 50 MB sein. Darüber hinaus sollte die Gesamtanzahl der Zeilen 500.000 nicht überschreiten. Diese Beschränkung stellt sicher, dass Server nicht mit zu vielen Anfragen überflutet werden.
* Sie können mehrere Dateien senden. Die Gesamtsumme der Zeilen aller Dateien, die Sie an einen Tag senden, sollte jedoch für jeden Kunden nicht mehr als eine Million betragen.
* Die Anzahl der Attribute, die Sie hochladen, ist unbegrenzt. Die Gesamtgröße eines Profils einschließlich der Systemdaten sollte jedoch 2000 KB nicht überschreiten. [!DNL Adobe] empfiehlt, weniger als 1000 KB Speicher für Profilattribute zu verwenden.
* Bei Parametern und Werten wird zwischen Groß- und Kleinschreibung unterschieden.

## HTTP-POST-Anfrage

Stellen Sie eine HTTP-POST-Anfrage an [!DNL Target] Edge-Server zur Verarbeitung der Datei. Hier finden Sie eine Beispiel-HTTP-POST-Anfrage für die Datei batch.txt mit dem curl-Befehl:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Wo:

BATCH.TXT ist der Dateiname. CLIENTCODE: [!DNL Target] Client-Code.

Wenn Sie Ihren Clientcode nicht kennen, finden Sie im [!DNL Target] Benutzeroberflächen-Klick **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**. Der Clientcode wird im [!UICONTROL Kontodetails] Abschnitt.

### Inspect der Antwort

Die Profiles API gibt den Sendestatus des Batches zur Verarbeitung zusammen mit einem Link unter &quot;batchStatus&quot;an eine andere URL zurück, die den Gesamtstatus des jeweiligen Batch-Auftrags anzeigt.

### Beispiel-API-Antwort

Der folgende Code wurde als Beispiel für eine Antwort der Profiles API verwendet:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

Wenn ein Fehler auftritt, enthält die Antwort `success=false` und eine detaillierte Fehlermeldung.

### Standard-Batch-Statusantwort

Eine erfolgreiche Standardantwort bei der obigen `batchStatus` Der URL-Link, auf den geklickt wird, sieht wie folgt aus:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Die erwarteten Werte für die Statusfelder sind:

| Status | Details |
| --- | --- |
| [!UICONTROL complete] | Die Anfrage zur Profil-Batch-Aktualisierung wurde erfolgreich abgeschlossen. |
| [!UICONTROL unvollständig] | Die Anfrage zur Profil-Batch-Aktualisierung wird weiterhin verarbeitet und nicht abgeschlossen. |
| [!UICONTROL hängenbleiben] | Die Anfrage zur Aktualisierung des Profil-Batches ist hängen geblieben und konnte nicht abgeschlossen werden. |

### Detaillierte Antwort der Batch-Status-URL

Eine detailliertere Antwort kann durch Übergabe eines Parameters abgerufen werden. `showDetails=true` der `batchStatus` URL weiter oben.

Beispiel:

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### Detaillierte Antwort

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
