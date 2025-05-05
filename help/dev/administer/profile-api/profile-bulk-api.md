---
title: Adobe Target-API zur Massenaktualisierung von Profilen
description: Erfahren Sie, wie Sie  [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] verwenden, um die Profildaten mehrerer Besucher zur Verwendung  [!DNL Target]  Targeting an zu senden.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: bee8752dd212a14f8414879e03565867eb87f6b9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 8%

---

# [!DNL Adobe Target Bulk Profile Update API]

Mit dem [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] können Sie Benutzerprofile für mehrere Besucher einer Website mithilfe einer Batch-Datei stapelweise aktualisieren.

Mit dem [!UICONTROL Bulk Profile Update API] können Sie bequem detaillierte Besucherprofildaten in Form von Profilparametern senden, damit viele Benutzer aus beliebigen externen Quellen [!DNL Target] können. Zu den externen Quellen können CRM (Customer Relationship Management)- oder POS (Point of Sale)-Systeme gehören, die normalerweise nicht auf einer Web-Seite verfügbar sind.

| Version  | URL-Beispiel | Funktionen |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | Unterstützung nur für die Massenaktualisierung von Profilen. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Profil erstellen, wenn nicht gefunden.</li><li>Statusaktualisierung pro Zeile.</li></ul> |

>[!NOTE]
>
>Version 2 (v2) des [!UICONTROL Bulk Profile Update API] ist die aktuelle Version. [!DNL Target] unterstützt jedoch weiterhin Version 1 (v1).

## Vorteile der Bulk Profile Update API

* Keine Begrenzung der Anzahl der Profilattribute.
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen

* Die Batch-Datei muss kleiner als 50 MB sein. Außerdem sollte die Gesamtzeilenzahl 500.000 Zeilen pro Upload nicht überschreiten.
* Aktualisierungen werden im Allgemeinen in weniger als einer Stunde durchgeführt, es kann jedoch bis zu 24 Stunden dauern, bis sie widergespiegelt werden.
* Es gibt keine Begrenzung für die Anzahl der Zeilen, die Sie in nachfolgenden Batches über einen Zeitraum von 24 Stunden hochladen können. Allerdings kann der Importverlauf während der Geschäftszeiten gedrosselt werden, um sicherzustellen, dass andere Prozesse effizient ablaufen.
* Aufeinander folgende Batch-Aktualisierungsaufrufe der Version 2 ohne dazwischen liegende Mbox-Aufrufe für dieselben ThirdPartyIds überschreiben die Eigenschaften, die beim ersten Batch-Aktualisierungsaufruf aktualisiert wurden.
* [!DNL Adobe] garantiert nicht, dass 100 % der Batch-Profildaten in Target integriert und aufbewahrt werden und somit für die Verwendung in der Zielgruppenbestimmung verfügbar sind. Beim aktuellen Design besteht die Möglichkeit, dass ein kleiner Prozentsatz der Daten (bis zu 0,1 % der großen Produktionschargen) nicht integriert oder aufbewahrt wird.

## Batch-Datei

Um Profildaten stapelweise zu aktualisieren, erstellen Sie eine Batch-Datei. Die Batch-Datei ist eine Textdatei mit Werten, die durch Kommas getrennt sind, ähnlich der folgenden Beispieldatei.

``` ```
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``` ```

>[!NOTE]
>
>Der `batch=` ist erforderlich und muss am Anfang der Datei angegeben werden.

Sie verweisen im Dateiaufruf an [!DNL Target] Server auf diese POST, um die Datei zu verarbeiten. Beachten Sie beim Erstellen der Batch-Datei Folgendes:

* In der ersten Zeile der Datei müssen die Spaltenüberschriften angegeben werden.
* Die erste Kopfzeile sollte entweder ein `pcId` oder ein `thirdPartyId` sein. Die [!UICONTROL Marketing Cloud visitor ID] wird nicht unterstützt. [!UICONTROL pcId] ist eine [!DNL Target] Besucher-ID. `thirdPartyId` ist eine von der Client-Anwendung angegebene ID, die über einen Mbox-Aufruf als `mbox3rdPartyId` an [!DNL Target] übergeben wird. Sie muss hier als `thirdPartyId` bezeichnet werden.
* Parameter und Werte, die Sie in der Batch-Datei angeben, müssen aus Sicherheitsgründen mit UTF-8 URL-codiert sein. Parameter und Werte können zur Verarbeitung über HTTP-Anfragen an andere Edge-Knoten weitergeleitet werden.
* Die Parameter dürfen nur das Format `paramName` haben. Parameter werden in [!DNL Target] als `profile.paramName` angezeigt.
* Wenn Sie [!UICONTROL Bulk Profile Update API] v2 verwenden, müssen Sie nicht alle Parameterwerte für jede `pcId` angeben. Profile werden für alle `pcId` oder `mbox3rdPartyId` erstellt, die nicht in [!DNL Target] gefunden werden. Wenn Sie v1 verwenden, werden Profile nicht für fehlende pcIds oder mbox3rdPartyIds erstellt.
* Die Batch-Datei muss kleiner als 50 MB sein. Darüber hinaus sollte die Gesamtzahl der Zeilen 500.000 nicht überschreiten. Dadurch wird sichergestellt, dass Server nicht mit zu vielen Anfragen überflutet werden.
* Sie können mehrere Dateien senden. Die Summe der Zeilen aller Dateien, die Sie an einem Tag senden, sollte jedoch eine Million pro Client nicht überschreiten.
* Die Anzahl der Attribute, die Sie hochladen können, ist nicht beschränkt. Die Gesamtgröße der externen Profildaten, zu denen Kundenattribute, Profil-API, In-Mbox-Profilparameter und Profilskriptausgabe gehören, darf jedoch 64 KB nicht überschreiten.
* Bei Parametern und Werten wird zwischen Groß- und Kleinschreibung unterschieden.

## HTTP-POST-Anfrage

Stellen Sie eine HTTP-Dateianforderung an [!DNL Target] Edge-Server, um die POST zu verarbeiten. Im Folgenden finden Sie eine Beispiel-HTTP-POST-Anfrage für die Datei batch.txt mit dem curl-Befehl:

``` ```
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``` ```

Wo:

BATCH.TXT ist der Dateiname. CLIENTCODE ist der [!DNL Target] Clientcode.

Wenn Sie Ihren Client-Code nicht kennen, klicken Sie in der [!DNL Target]-Benutzeroberfläche auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Der Client-Code wird im Abschnitt [!UICONTROL Account Details] angezeigt.

### Inspect - die Antwort

Die Profile-API gibt den Übermittlungsstatus des Batches zur Verarbeitung zusammen mit einem Link unter „batchStatus“ zu einer anderen URL zurück, die den Gesamtstatus des jeweiligen Batch-Vorgangs anzeigt.

### Beispiel einer API-Antwort

Der folgende Code-Ausschnitt ist ein Beispiel für eine Profile-API-Antwort:

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

Wenn ein Fehler auftritt, enthält die Antwort `success=false` und eine detaillierte Fehlermeldung.

### Standardmäßige Batch-Statusantwort

Eine erfolgreiche Standardantwort beim Klicken auf den obigen `batchStatus`-URL-Link sieht wie folgt aus:

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

Erwartete Werte für die Statusfelder sind:

| Status | Details |
| --- | --- |
| [!UICONTROL complete] | Die Anfrage zur Aktualisierung des Profil-Batches wurde erfolgreich abgeschlossen. |
| [!UICONTROL incomplete] | Die Anfrage zur Aktualisierung des Profil-Batches wird noch verarbeitet und nicht abgeschlossen. |
| [!UICONTROL stuck] | Die Anfrage zur Aktualisierung des Profil-Batches ist hängen geblieben und konnte nicht abgeschlossen werden. |

### Detaillierte Batch-Status-URL-Antwort

Sie können eine detailliertere Antwort abrufen, indem Sie einen `showDetails=true` an die oben `batchStatus` URL übergeben.

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
