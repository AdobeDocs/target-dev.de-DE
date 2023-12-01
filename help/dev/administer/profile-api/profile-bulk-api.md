---
title: Adobe Target Bulk-Profil-Update-API
description: Verwendung von [!DNL Adobe Target] [!UICONTROL Bulk-Profil-Update-API] zum Senden mehrerer Besucherprofildaten an [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 6f7d9875e3b73352ead3a55e40a4b2f81f3d4400
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 9%

---

# [!DNL Adobe Target Bulk Profile Update API]

Die [!DNL Adobe Target] [!UICONTROL Bulk-Profil-Update-API] ermöglicht Ihnen, mithilfe einer Batch-Datei Benutzerprofile für mehrere Besucher einer Website stapelweise zu aktualisieren.

Verwenden der [!UICONTROL Bulk-Profil-Update-API]können Sie detaillierte Besucherprofildaten in Form von Profilparametern für viele Benutzer an senden. [!DNL Target] aus einer beliebigen externen Quelle. Externe Quellen können beispielsweise CRM-Systeme (Customer Relationship Management) oder POS-Systeme (Point of Sale) sein, die normalerweise nicht auf einer Webseite verfügbar sind.

| Version  | URL-Beispiel | Funktionen |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | Nur Unterstützung für Massenaktualisierung von Profilen. |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>Erstellen Sie ein Profil, falls nicht gefunden.</li><li>Aktualisierung des Zeilenstatus.</li></ul> |

>[!NOTE]
>
>Version 2 (v2) der [!UICONTROL Bulk-Profil-Update-API] ist die aktuelle Version. Allerdings [!DNL Target] unterstützt weiterhin Version 1 (v1).

## Einschränkungen

* Die Batch-Datei muss kleiner als 50 MB sein. Außerdem sollte die Gesamtzeilenzahl 500.000 Zeilen pro Upload nicht überschreiten.
* Die Anzahl der Zeilen, die Sie über einen Zeitraum von 24 Stunden in nachfolgenden Batches hochladen können, ist nicht beschränkt. Allerdings kann der Importverlauf während der Geschäftszeiten gedrosselt werden, um sicherzustellen, dass andere Prozesse effizient ablaufen.
* Aufeinander folgende v2-Batch-Aktualisierungsaufrufe ohne dazwischen liegende Mbox-Aufrufe für dieselben thirdPartyIds überschreiben die Eigenschaften, die im ersten Batch-Aktualisierungsaufruf aktualisiert wurden.

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
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate
``````

Wo:

BATCH.TXT ist der Dateiname. CLIENTCODE: [!DNL Target] Client-Code.

Wenn Sie Ihren Clientcode nicht kennen, finden Sie im [!DNL Target] Benutzeroberflächen-Klick **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**. Der Clientcode wird im [!UICONTROL Kontodetails] Abschnitt.

### Inspect der Antwort

v2 gibt den Status nach Profil zurück und v1 gibt nur den Gesamtstatus zurück. Die Antwort enthält einen Link zu einer anderen URL mit der Erfolgsmeldung &quot;Profil für Profil&quot;.

### Beispielantwort

```
true http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00 Batch submitted for processing
```

Wenn ein Fehler auftritt, enthält die Antwort `success=false` und eine detaillierte Fehlermeldung.

Eine erfolgreiche Antwort sieht wie folgt aus:

``````
demo-1845664501 1436187396849-250353.03_03 success 2403081156529-351655.03_03 success 2403081156529-351656.03_03 success 1436187396849-250351.01_00 success 
``````

Die erwarteten Werte für die Statusfelder sind:

**success**: Das Profil wurde aktualisiert. Wenn das Profil nicht gefunden wurde, wurde eines mit den Werten aus dem Batch erstellt.
**error**: Das Profil wurde aufgrund eines Fehlers, einer Ausnahme oder eines Nachrichtenverlusts nicht aktualisiert oder erstellt.
**pending**: Das Profil wurde noch nicht aktualisiert oder erstellt.



