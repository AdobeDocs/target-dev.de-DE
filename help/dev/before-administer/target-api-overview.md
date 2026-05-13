---
title: Übersicht über die Adobe Target-API
description: Überblick über die verschiedenen Adobe Target-APIs, einschließlich Bereitstellungs-API, Reporting-API, Admin-API, Profil-API, Recommendations-API und Links zu Postman-Sammlungen.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/GbrWhrZxH-sTtpxotpJGbr-sHuIXrX7rZFQhju76-vM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 448
ht-degree: 0%

---

# Target-API - Übersicht

In diesem Artikel werden die verschiedenen Target-APIs im Allgemeinen beschrieben, bevor Sie sich auf die spezifischen Anforderungen der Admin- und Profil-APIs konzentrieren. Wenn Sie Target über die Benutzeroberfläche verwalten möchten, finden Sie weitere Informationen im Abschnitt [Administration“ des *Adobe Target Business-Benutzerhandbuchs*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=de).

## API-Typen

Die Adobe Target-APIs sind eine Sammlung von APIs, die Adobe Target-Produkte wie Adobe Recommendations unterstützen. Diese APIs ermöglichen die Erstellung von datenreichen Benutzeroberflächen, die Sie zum Bearbeiten und Integrieren von Daten verwenden können.

Adobe Target-APIs können nach Typ gruppiert werden: Admin, Profil, Bereitstellung und Reporting.

>[!NOTE]
>
>Die Admin-APIs und Profil-APIs werden häufig gemeinsam bezeichnet („Admin- und Profil-APIs„), können aber auch separat bezeichnet werden („Admin-APIs“ und „Profil-APIs„). Die Recommendations-API ist eine spezifische Implementierung einer Target Admin-API.

| API-Typ | Was sie Ihnen ermöglicht zu tun | Downloadlink | Weitere hilfreiche Links |
| --- | --- | --- |--- |
| [Admin](../administer/admin-api/admin-api-overview-new.md) | Aktivitäten, Zielgruppen, Angebote und andere Objekte (einschließlich Recommendations-Entitäten, Kriterien, Designs usw.) erstellen, ändern und löschen. Die Recommendations-APIs sind eine Art Admin-API.) | <UL><li>[Target Admin-API - Postman-Sammlung](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations-API - Postman-Sammlung](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Verwenden von Recommendations-APIs](../before-administer/recs-api/overview.md) |
| Profil | Abrufen und Ändern von in Adobe Target gespeicherten Benutzerprofilen. | [Postman-Sammlung der Target-Profil-API](https://developers.adobetarget.com/api/#profiles) |  |
| [Bereitstellung](../implement/delivery-api/overview.md) | Rufen Sie optimierte und personalisierte Inhalte von Target ab, die an einen Endbenutzer gesendet werden sollen. | [Postman-Sammlung der Target-Bereitstellungs-API](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Berichterstellung](../administer/admin-api/admin-api-overview-new.md) | Exportieren Sie Aktivitätsergebnisse und andere Berichterstellungsergebnisse. | Reporting-APIs sind in der Sammlung [Target Admin-API Postman](https://developers.adobetarget.com/api/#admin-postman-collection) enthalten. |  |
| [Modelle](../administer/models-api/models-api-overview.md) | Verwalten Sie die Liste der Funktionen, die Target aus seinen Modellen für maschinelles Lernen ausschließen soll (die &quot;Blockierungsliste„). Die Models-API ist eine Art Admin-API, sie wird hier jedoch aufgrund ihrer eindeutigen Vorgänge bei Objekten (Blockierungslisten), auf die nicht über die Benutzeroberfläche zugegriffen werden kann, separat aufgeführt. |  |  |

## API-Unterschiede

Es gibt wichtige Unterschiede zwischen Target Admin-APIs (einschließlich der Recommendations-APIs) und Target-Bereitstellungs-APIs:

* Mit Admin-APIs können Sie verschiedene Aspekte von Target konfigurieren, die Sie auch in der Target-Benutzeroberfläche konfigurieren können. Die Ausnahme bildet die Models-API, mit der Sie Aspekte von Target konfigurieren können, die nicht in der Benutzeroberfläche verfügbar sind. Unabhängig davon **alle Admin-APIs müssen authentifiziert werden.**

* Mit Bereitstellungs-APIs können Sie Inhalte abrufen. Bereitstellungs-APIs erfordern keine Authentifizierung.

Um Target Admin-APIs verwenden zu können, müssen Sie die Authentifizierung mithilfe der [Adobe Developer Console](https://developer.adobe.com/console/home) konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung](../before-administer/configure-authentication.md).
