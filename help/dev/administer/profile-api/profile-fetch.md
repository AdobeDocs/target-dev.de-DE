---
title: Profile abrufen
description: Erfahren Sie, wie Sie mit den Adobe Target-Profil-APIs Besucherdaten abrufen können, um sie in [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---

# Profilaktualisierung

A [!DNL Target] Profile können auf zwei Arten abgerufen werden: mithilfe eines `tntid` oder `thirdPartyId`.

## Verwenden einer tntid

[!DNL Target] weist automatisch eine `tntid` für jede Anfrage.

Das folgende Beispiel zeigt das Anforderungsformat zum Abrufen eines Profils mithilfe eines `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

Ersetzen `<your-client-code>` und `your-tnt-id` und eine GET-Anfrage auslösen. Im Folgenden finden Sie ein Beispiel für einen Profilabruf mit einem `tntid`;

```
http://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## Verwenden einer thirdPartyId

[!DNL Adobe Target] Profile können mit Ihrer eigenen Kennung (z. B. CRM-ID, `uuid`, Mitgliedsnummer usw.).

Siehe [Profile aktualisieren](/help/dev/administer/profile-api/profile-api-overview.md) um zu erfahren, wie Sie eine `thirdPartyId` zu Ihrem Profil.

Das folgende Beispiel zeigt das Anforderungsformat zum Abrufen eines Profils mithilfe eines `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

Ersetzen `<your-client-code>` und `your-thirdpartyid` und eine GET-Anfrage auslösen. Im Folgenden finden Sie ein Beispiel für einen Profilabruf mit einem [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

Wenn dieser Aufruf erfolgt, [!DNL Target] versucht, das Profil zuerst im Cluster zu finden, das in der Edge-Anfrage angegeben ist, oder wo sich das Profil befindet, und den Inhalt zurückzugeben. Der Profilinhalt wird im JSON-Format zurückgegeben.

## Authentifizierung

Die [!DNL Target Profile API] kann gesichert werden, indem die Authentifizierung über die [!DNL Target] Benutzeroberfläche, wie hier beschrieben. Nachdem die Authentifizierung aktiviert wurde, muss für alle Profil-API-Anfragen das Profilauthentifizierungstoken in den Anfragekopfzeilen festgelegt sein. Das Token selbst kann mithilfe der [!DNL Target] Benutzeroberfläche oder unter Verwendung der oben im Abschnitt [Profilauthentifizierungstoken](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} Abschnitt.

## Metriken

Diese Aufrufe zählen nicht zu Ihren Mbox-Aufrufen.

## Umgang mit Fehlern

Im Falle eines Aufrufs an `/thirdPartyId` mit ungültigen oder abgelaufenen `thirdPartyId` spezifiziert:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

Wenn das Profil nicht gefunden werden kann oder abgelaufen ist:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
