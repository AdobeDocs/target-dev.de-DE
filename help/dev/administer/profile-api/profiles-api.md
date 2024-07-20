---
title: Adobe Target-Profiles-API
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten an  [!DNL Target] senden können.
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] Übersicht

[!DNL Adobe Target] erstellt und verwaltet ein Profil für jeden einzelnen Benutzer. Dieses Profil wird im Edge-Cluster [!DNL Target] gespeichert und nach jedem Besuch in Echtzeit aktualisiert.

## Struktur eines [!DNL Target] -Profils

Ein Target -Profil besteht aus den folgenden Objekten:

| Objekt | Details |
| --- | --- |
| `clientcode` | Der [!DNL Target]-Clientcode, mit dem das Profil verknüpft ist. |
| `visitorId` | Die Kennung für das Profil. Dies kann ein `tntid`, `thirdpartyid` oder `marketingcloudvisitorid` sein. |
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
