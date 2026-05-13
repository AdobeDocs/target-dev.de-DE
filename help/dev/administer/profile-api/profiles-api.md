---
title: Adobe Target Profile-API
description: Erfahren Sie, wie Sie mit Adobe Target-Profil-APIs Besucherdaten an  [!DNL Target] senden.
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
TQID: https://experienceleague.adobe.com/zmA1vGqBRL8gD-cFjJC0idogx7UF1e22iLEfNT9OHZ4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 105
ht-degree: 2%

---

# Übersicht über [!DNL Adobe Target Profiles API]

[!DNL Adobe Target] erstellt und verwaltet ein Profil für jeden einzelnen Benutzer. Dieses Profil wird im [!DNL Target] Edge-Cluster gespeichert und nach jedem Besuch in Echtzeit aktualisiert.

## Struktur eines [!DNL Target]

Ein Zielprofil besteht aus den folgenden Objekten:

| Objekt | Details |
| --- | --- |
| `clientcode` | Der [!DNL Target] Clientcode, mit dem das Profil verknüpft ist. |
| `visitorId` | Die Kennung für das Profil. Dabei kann es sich um einen `tntid`, einen `thirdpartyid` oder einen `marketingcloudvisitorid` handeln. |
| `modifiedAt` | Der Zeitstempel der letzten Aktualisierung des Profils. |
| `profileAttributes` | Liste aller Profilattribute, die als Schlüssel-Wert-Paare in diesem einzelnen Profil gespeichert werden. |

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
