---
title: Adobe Target Bulk-Profil-Update-API
description: Erfahren Sie, wie Sie mit  [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] die Profildaten mehrerer Besucher zur Verwendung beim Targeting an [!DNL Target] senden können.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: bee8752dd212a14f8414879e03565867eb87f6b9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

Mit dem Wert [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] können Sie mithilfe einer Stapelverarbeitungsdatei Benutzerprofile für mehrere Besucher einer Website stapelweise aktualisieren.

Mit dem [!UICONTROL Bulk Profile Update API] können Sie bequem detaillierte Besucherprofildaten in Form von Profilparametern für viele Benutzer von jeder externen Quelle an [!DNL Target] senden. Externe Quellen können beispielsweise CRM-Systeme (Customer Relationship Management) oder POS-Systeme (Point of Sale) sein, die normalerweise nicht auf einer Webseite verfügbar sind.

| Version  | URL-Beispiel | Funktionen |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Nur Unterstützung für Massenaktualisierung von Profilen. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Erstellen Sie ein Profil, falls nicht gefunden.</li><li>Aktualisierung des Zeilenstatus.</li></ul> |

>[!NOTE]
>
>Version 2 (v2) von [!UICONTROL Bulk Profile Update API] ist die aktuelle Version. Allerdings unterstützt [!DNL Target] weiterhin Version 1 (v1).

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
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``````

>[!NOTE]
>
>Der Parameter `batch=` ist erforderlich und muss am Anfang der Datei angegeben werden.

Sie verweisen auf diese POST im Dateiaufruf an [!DNL Target] -Server, um die Datei zu verarbeiten. Beachten Sie beim Erstellen der Batch-Datei Folgendes:

* In der ersten Zeile der Datei müssen Spaltenüberschriften angegeben werden.
* Die erste Kopfzeile sollte entweder `pcId` oder `thirdPartyId` sein. Die [!UICONTROL Marketing Cloud visitor ID] wird nicht unterstützt. [!UICONTROL pcId] ist eine [!DNL Target] generierte visitorID. `thirdPartyId` ist eine von der Clientanwendung angegebene ID, die über einen Mbox-Aufruf als `mbox3rdPartyId` an [!DNL Target] übergeben wird. Sie muss hier als `thirdPartyId` bezeichnet werden.
* Die in der Batch-Datei angegebenen Parameter und Werte müssen aus Sicherheitsgründen mit UTF-8 URL-kodiert werden. Parameter und Werte können zur Verarbeitung über HTTP-Anforderungen an andere Edge-Knoten weitergeleitet werden.
* Die Parameter dürfen nur das Format `paramName` aufweisen. Parameter werden in [!DNL Target] als `profile.paramName` angezeigt.
* Wenn Sie [!UICONTROL Bulk Profile Update API] v2 verwenden, müssen Sie nicht alle Parameterwerte für jeden `pcId` angeben. Profile werden für alle `pcId` oder `mbox3rdPartyId` erstellt, die nicht in [!DNL Target] gefunden werden. Wenn Sie v1 verwenden, werden Profile nicht für fehlende pcIds oder mbox3rdPartyIds erstellt.
* Die Batch-Datei muss kleiner als 50 MB sein. Darüber hinaus sollte die Gesamtanzahl der Zeilen 500.000 nicht überschreiten. Diese Beschränkung stellt sicher, dass Server nicht mit zu vielen Anfragen überflutet werden.
* Sie können mehrere Dateien senden. Die Gesamtsumme der Zeilen aller Dateien, die Sie an einen Tag senden, sollte jedoch für jeden Kunden nicht mehr als eine Million betragen.
* Die Anzahl der Attribute, die Sie hochladen können, ist nicht beschränkt. Die Gesamtgröße der externen Profildaten, einschließlich Kundenattributen, Profil-API, In-Mbox-Profilparametern und Profilskriptausgabe, darf jedoch 64 KB nicht überschreiten.
* Bei Parametern und Werten wird zwischen Groß- und Kleinschreibung unterschieden.

## HTTP-POST-Anfrage

Stellen Sie eine HTTP-POST-Anfrage an die [!DNL Target] -Edge-Server, um die Datei zu verarbeiten. Hier finden Sie eine Beispiel-HTTP-POST-Anfrage für die Datei batch.txt mit dem curl-Befehl:

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

Wo:

BATCH.TXT ist der Dateiname. CLIENTCODE ist der [!DNL Target]-Clientcode.

Wenn Sie Ihren Clientcode nicht kennen, klicken Sie in der [!DNL Target] -Benutzeroberfläche auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Der Clientcode wird im Abschnitt [!UICONTROL Account Details] angezeigt.

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

Eine erfolgreiche Standardantwort, wenn auf den obigen URL-Link `batchStatus` geklickt wird, sieht wie folgt aus:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Die erwarteten Werte für die Statusfelder sind:

| Status | Details |
| --- | --- |
| [!UICONTROL complete] | Die Anfrage zur Profil-Batch-Aktualisierung wurde erfolgreich abgeschlossen. |
| [!UICONTROL incomplete] | Die Anfrage zur Profil-Batch-Aktualisierung wird weiterhin verarbeitet und nicht abgeschlossen. |
| [!UICONTROL stuck] | Die Anfrage zur Aktualisierung des Profil-Batches ist hängen geblieben und konnte nicht abgeschlossen werden. |

### Detaillierte Antwort der Batch-Status-URL

Eine detailliertere Antwort kann abgerufen werden, indem ein Parameter `showDetails=true` an die obige `batchStatus` -URL übergeben wird.

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
