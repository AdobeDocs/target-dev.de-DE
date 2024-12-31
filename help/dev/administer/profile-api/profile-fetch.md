---
title: Profile abrufen
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten abrufen können, die in verwendet werden [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Profile abrufen

Ein [!DNL Target] kann auf drei Arten abgerufen werden: mithilfe eines `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` oder `thirdPartyId`.

## Verwenden einer [!DNL Experience Cloud Visitor ID] (ECID)

Basierend auf dem `ECID` können Sie ein Profil abrufen. Die HTTP-Methode muss GET lauten.

Die URL sieht wie im folgenden Beispiel aus:

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

Ersetzen Sie `<clientCode>` durch Ihre [!DNL Target] [!UICONTROL Client Code] und `<ECID>` durch Ihre [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## Verwenden einer tntid

[!DNL Target] weist jeder Anfrage automatisch einen `tntid` zu.

Das folgende Beispiel zeigt das Anfrageformat zum Abrufen eines Profils mithilfe eines `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Ersetzen Sie `<your-client-code>` und `your-tnt-id` und lösen Sie eine GET-Anfrage aus. Im Folgenden finden Sie ein Beispiel für einen Aufruf zum Abrufen von Profilen mit einem `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Verwenden einer ThirdPartyId

[!DNL Adobe Target] können mit Ihrer eigenen Kennung erweitert werden (z. B. CRM-ID, `uuid`, Mitgliedschaftsnummer usw.).

Unter [Aktualisieren von Profilen](/help/dev/administer/profile-api/profile-api-overview.md) erfahren Sie, wie Sie ein `thirdPartyId` an Ihr Profil anhängen können.

Das folgende Beispiel zeigt das Anfrageformat zum Abrufen eines Profils mithilfe eines `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Ersetzen Sie `<your-client-code>` und `your-thirdpartyid` und lösen Sie eine GET-Anfrage aus. Im Folgenden finden Sie ein Beispiel für einen Aufruf zum Abrufen von Profilen mit einem [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Wenn dieser Aufruf erfolgt, versucht [!DNL Target], das Profil zuerst in dem Cluster zu finden, der in der Edge-Anfrage angegeben ist, oder dort, wo sich das Profil befindet, und den Inhalt zurückzugeben. Die Profilinhalte werden im JSON-Format zurückgegeben.

## Authentifizierung

Das [!DNL Target Profile API] kann gesichert werden, indem die Authentifizierung über die [!DNL Target]-Benutzeroberfläche aktiviert wird, wie hier beschrieben. Sobald die Authentifizierung aktiviert ist, muss bei allen Profil-API-Anfragen das Profil-Authentifizierungstoken in den Anfragekopfzeilen festgelegt sein. Das Token selbst kann über die [!DNL Target]-Benutzeroberfläche oder mithilfe der oben im Abschnitt &quot;[-Authentifizierungstoken“ ](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} Schritte generiert werden.

## Messung

Diese Aufrufe werden nicht für Ihre Mbox-Aufrufe gezählt.

## Fehlerbehandlung

Bei einem Aufruf von `/thirdPartyId` mit einer ungültigen oder abgelaufenen `thirdPartyId`:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Wenn das Profil nicht gefunden werden kann oder abgelaufen ist:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
