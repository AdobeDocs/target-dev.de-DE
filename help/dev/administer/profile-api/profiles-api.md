---
title: Adobe Target-Profiles-API
description: Erfahren Sie, wie Sie mit Adobe Target Profile-APIs Besucherdaten an senden können. [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] Übersicht

[!DNL Adobe Target] erstellt und verwaltet ein Profil für jeden einzelnen Benutzer. Dieses Profil wird im [!DNL Target] Edge-Cluster und wird in Echtzeit nach jedem Besuch aktualisiert.

## Struktur einer [!DNL Target] profile

Ein Target -Profil besteht aus den folgenden Objekten:

| Objekt | Details |
| --- | --- |
| `clientcode` | Die [!DNL Target] Client-Code, mit dem das Profil verknüpft ist. |
| `visitorId` | Die Kennung für das Profil. Dies kann eine `tntid`, `thirdpartyid`oder `marketingcloudvisitorid`. |
| `modifiedAt` | Der Zeitstempel der letzten Aktualisierung des Profils. |
| `profileAttributes` | Liste aller Profilattribute, die als Schlüssel-Wert-Paare für das jeweilige Profil gespeichert sind. |

### Beispielprofilstruktur

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
