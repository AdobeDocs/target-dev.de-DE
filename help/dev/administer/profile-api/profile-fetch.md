---
title: Profile abrufen
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten zur Verwendung in [!DNL Target] abrufen können.
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Profile abrufen

Ein [!DNL Target] -Profil kann auf drei Arten abgerufen werden: mit einem `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` oder `thirdPartyId`.

## Verwenden von [!DNL Experience Cloud Visitor ID] (ECID)

Sie können ein Profil abrufen, das auf dem `ECID` basiert. Die HTTP-Methode muss GET sein.

Die URL sieht wie folgt aus:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Ersetzen Sie `<clientCode>` durch Ihre [!DNL Target] [!UICONTROL Client Code] und `<ECID>` durch Ihre [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Verwenden einer tntid

[!DNL Target] weist automatisch eine `tntid` für jede Anfrage zu.

Das folgende Beispiel zeigt das Anforderungsformat zum Abrufen eines Profils mit dem Wert `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Ersetzen Sie `<your-client-code>` und `your-tnt-id` und lösen Sie eine GET-Anfrage aus. Im Folgenden finden Sie ein Beispiel für einen Profilabruf mit einem `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Verwenden einer thirdPartyId

[!DNL Adobe Target] -Profile können mit Ihrer eigenen Kennung erweitert werden (z. B. CRM-ID, `uuid`, Mitgliedsnummer usw.).

Unter [Profile aktualisieren](/help/dev/administer/profile-api/profile-api-overview.md) erfahren Sie, wie Sie Ihrem Profil eine `thirdPartyId` anhängen können.

Das folgende Beispiel zeigt das Anforderungsformat zum Abrufen eines Profils mit dem Wert `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Ersetzen Sie `<your-client-code>` und `your-thirdpartyid` und lösen Sie eine GET-Anfrage aus. Im Folgenden finden Sie ein Beispiel für einen Profilabruf mit einem [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Wenn dieser Aufruf erfolgt, versucht [!DNL Target], das Profil zuerst im Cluster zu finden, das in der Edge-Anfrage vermerkt ist, oder, wo sich das Profil befindet, und den Inhalt zurückzugeben. Der Profilinhalt wird im JSON-Format zurückgegeben.

## Authentifizierung

Der [!DNL Target Profile API] kann gesichert werden, indem die Authentifizierung über die [!DNL Target] -Benutzeroberfläche aktiviert wird, wie hier beschrieben. Nachdem die Authentifizierung aktiviert wurde, muss für alle Profil-API-Anfragen das Profilauthentifizierungstoken in den Anfragekopfzeilen festgelegt sein. Das Token selbst kann mithilfe der Benutzeroberfläche von [!DNL Target] oder mithilfe der oben im Abschnitt [Profilauthentifizierungstoken](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} erläuterten Schritte generiert werden.

## Metriken

Diese Aufrufe zählen nicht zu Ihren Mbox-Aufrufen.

## Umgang mit Fehlern

Im Falle eines Aufrufs von `/thirdPartyId` mit einer ungültigen oder abgelaufenen `thirdPartyId`:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Wenn das Profil nicht gefunden werden kann oder abgelaufen ist:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
