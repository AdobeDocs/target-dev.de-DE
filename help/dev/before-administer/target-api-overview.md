---
title: Übersicht über die Adobe Target API
description: Übersicht über die verschiedenen Adobe Target-APIs, einschließlich Versand-API, Reporting-API, Admin-API, Profil-API, Recommendations-API und Links zu Postman-Sammlungen.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Target-API - Übersicht

In diesem Artikel werden die verschiedenen Target-APIs im Allgemeinen beschrieben, bevor der Schwerpunkt auf die spezifischen Anforderungen für die Admin- und Profil-APIs gelegt wird. Wenn Sie Target über die Benutzeroberfläche verwalten möchten, lesen Sie den Abschnitt [Administration des *Adobe Target Business User Guide*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## API-Typen

Bei den Adobe Target-APIs handelt es sich um eine Sammlung von APIs, die für Adobe Target-Produkte wie Adobe Recommendations verwendet werden. Diese APIs ermöglichen die Erstellung datenreicher Benutzeroberflächen, mit denen Sie Daten bearbeiten und integrieren können.

Adobe Target-APIs können nach Typ gruppiert werden: Admin, Profil, Versand und Berichterstellung.

>[!NOTE]
>
>Die Admin-APIs und Profil-APIs werden häufig kollektiv bezeichnet (&quot;Admin- und Profil-APIs&quot;), können aber auch separat referenziert werden (&quot;Admin-APIs&quot;und &quot;Profil-APIs&quot;). Die Recommendations-API ist eine spezifische Implementierung einer Target Admin-API.

| API-Typ | Was es Ihnen ermöglicht | Downloadlink | Weitere hilfreiche Links |
| --- | --- | --- |--- |
| [Admin](../administer/admin-api/admin-api-overview-new.md) | Erstellen, ändern und löschen Sie Aktivitäten, Zielgruppen, Angebote und andere Objekte (einschließlich Recommendations-Entitäten, Kriterien, Designs usw.). Die Recommendations-APIs sind eine Art Admin-API.) | <UL><li>[Postman-Sammlung der Target-Admin-API](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [Verwenden von Recommendations-APIs](../before-administer/recs-api/overview.md) |
| Profil | Abrufen und Ändern von in Adobe Target gespeicherten Benutzerprofilen. | [Postman-Sammlung der Target-Profil-API](https://developers.adobetarget.com/api/#profiles) |  |
| [Bereitstellung](../implement/delivery-api/overview.md) | Rufen Sie optimierte und personalisierte Inhalte von Target für die Bereitstellung an einen Endbenutzer ab. | [Postman-Sammlung der Target-Bereitstellungs-API](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [Berichterstellung](../administer/admin-api/admin-api-overview-new.md) | Exportieren Sie Aktivitätsergebnisse und andere Berichtsergebnisse. | Reporting-APIs sind in der [Target Admin API Postman-Sammlung](https://developers.adobetarget.com/api/#admin-postman-collection) enthalten. |  |
| [Modelle](../administer/models-api/models-api-overview.md) | Verwalten Sie die Liste der Funktionen, die Target aus seinen maschinellen Lernmodellen ausschließen soll (die &quot;Blockierungsliste&quot;). Die Modelle-API ist eine Art Admin-API, wird hier jedoch separat aufgeführt, da sie eindeutig mit Objekten auf die Blockierungsliste setzt (), auf die über die Benutzeroberfläche nicht zugegriffen werden kann. |  |  |

## API-Unterschiede

Es gibt wichtige Unterschiede zwischen Target Admin-APIs (einschließlich der Recommendations-APIs) und Target-Bereitstellungs-APIs:

* Mit Admin-APIs können Sie verschiedene Aspekte von Target konfigurieren, die Sie auch in der Target-Benutzeroberfläche konfigurieren können. Eine Ausnahme bildet die Modelle-API, mit der Sie Aspekte von Target konfigurieren können, die nicht in der Benutzeroberfläche verfügbar sind. Unabhängig davon ist für **alle Admin-APIs eine Authentifizierung erforderlich.**

* Mit Bereitstellungs-APIs können Sie Inhalte abrufen. Bereitstellungs-APIs erfordern keine Authentifizierung.

Um Target Admin-APIs zu verwenden, müssen Sie die Authentifizierung mit [Adobe Developer Console](https://developer.adobe.com/console/home) konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung](../before-administer/configure-authentication.md).
