---
keywords: api, adobe i/o, classic, adobe developer console
description: Erfahren Sie, wie Sie von den [!DNL Adobe Target Classic] APIs zu den [!DNL Target] APIs auf der [!DNL Adobe Developer Console] wechseln.
title: Wie kann ich von [!DNL Target Classic] APIs zu [!DNL Target] APIs auf der  [!DNL Adobe Developer Console] wechseln?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Übergang von [!DNL Target Classic] APIs zu [!DNL Target] APIs auf der [!DNL Adobe Developer Console]

Informationen, die Sie beim Übergang von den [!DNL Target Classic] -APIs zu den [!DNL Target] -APIs auf der [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) unterstützen.

Mit der Stilllegung von [!DNL Adobe Target Classic] wurden die mit Ihrem [!DNL Target Classic]-Konto verbundenen APIs ebenfalls nicht mehr verfügbar gemacht. Dieser Artikel hilft Ihnen beim Übergang Ihrer [!DNL Target Classic] API-basierten Integrationen zu den [!DNL Target] APIs, die von [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) unterstützt werden.

Weitere Informationen zu [!DNL Target] APIs finden Sie unter [[!DNL Target] APIs](/help/dev/before-administer/target-api-overview.md). Weitere Informationen zu [!DNL Target] SDK finden Sie unter [[!DNL Target] Serverseitige Implementierung](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie  

| Begriff | Beschreibung |
|--- |--- |
| Klassische API | APIs, die mit Ihrem [!DNL Target Classic]-Konto verknüpft sind. Diese API-Aufrufe basieren auf einer Benutzername-und-Kennwort-basierten Authentifizierung und verwenden den Hostnamen `testandtarget.omniture.com`. Wenn Ihre API-Aufrufe einen Benutzernamen und ein Kennwort in der Anfrage-URL enthalten, müssen Sie zu den [!DNL Adobe Developer Console] -APIs wechseln. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | Der [!DNL Adobe Developer Console] ist das Gateway für [!DNL Target] -APIs. Diese APIs sind mit Ihrem [!DNL Target Standard/Premium]-Konto verbunden. Die [!DNL Target] -APIs für die [!DNL Adobe Developer Console] verwenden eine [JWT-basierte Authentifizierung](../../before-administer/configure-authentication.md), die dem Branchenstandard für sichere Enterprise-APIs entspricht. |

## Timeline 

Die folgenden APIs wurden bei der Stilllegung von [!DNL Target Classic] eingestellt:

| Datum | Details |
|--- |--- |
| 17. Oktober 2017 | Alle API-Methoden, die einen Schreibvorgang (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` und `setCampaignState`) durchführen, wurden beendet.<P>Dies ist dasselbe Datum, an dem alle [!DNL Target Classic] -Benutzerkonten auf schreibgeschützt gesetzt wurden. |
| 14. November 2017 | Die verbleibenden APIs wurden eingestellt. Dies ist das Datum, an dem die [!DNL Target Classic] -Benutzeroberfläche eingestellt wurde. |

[!DNL Recommendations Classic] APIs wurden von dieser Zeitleiste nicht beeinflusst.

## Äquivalente Methoden 

In der folgenden Tabelle sind die äquivalenten [!DNL Adobe Developer Console] -API-Methoden für die klassischen API-Methoden aufgeführt. Die [!DNL Adobe Developer Console] -APIs geben JSON zurück, während die klassischen APIs XML zurückgeben.

Die API-Methoden [!DNL Adobe Developer Console] sind mit dem entsprechenden Abschnitt auf der API-Dokumentations-Site verknüpft. Für jede API-Methode wird ein Beispiel angegeben. Sie können auch die [!DNL Target] Admin API Postman-Sammlung verwenden, die Beispiel-API-Aufrufe für alle Adobe-API-Methoden auf dem [!DNL Adobe Developer Console] enthält.

| Gruppierung | Klassische API-Methode | [!DNL Adobe Developer Console] API-Methode | Hinweise |
|--- |--- |--- |--- |
| Kampagne/Aktivität | Kampagnenerstellung | [AB-Aktivität erstellen](https://developers.adobetarget.com/api/#create-ab-activity)<P>[XT-Aktivität erstellen](https://developers.adobetarget.com/api/#create-xt-activity) | Die neuen APIs enthalten separate Erstellungsmethoden für AB und XT |
|  | Kampagnenaktualisierung | [AB-Aktivität aktualisieren](https://developers.adobetarget.com/api/#update-ab-activity)<P>[XT-Aktivität aktualisieren](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | Kampagne kopieren | K. A. | APIs zum Erstellen von Aktivitäten verwenden |
|  | Kampagnenliste | [Listenaktivitäten](https://developers.adobetarget.com/api/#list-activities) |  |
|  | Kampagnenstatus | [Aktivitätsstatus aktualisieren](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | Kampagnenansicht | [AB-Aktivität nach ID abrufen](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[XT-Aktivität nach ID abrufen](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | Drittanbieter-Kampagnen-ID | K. A. | Wenn Sie eine thirdpartyID verwenden, können die relevanten Aktivitätsmethoden verwendet werden |
| Angebote | Angebotserstellung | [Angebot erstellen](https://developers.adobetarget.com/api/#create-offer) |  |
|  | Angebotsabruf | [Angebot nach ID abrufen](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | Angebotsliste | [Angebote auflisten](https://developers.adobetarget.com/api/#list-offers) |  |
|  | Ordnerliste | K. A. | Ordner werden in [!DNL Target Standard/Premium] nicht unterstützt |
| Berichterstellung | Kampagnenleistungsbericht | [AB-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[XT-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Audit-Bericht | [Audit-Bericht abrufen](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | 1-1-Inhaltsbericht | [AP-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Kontoeinstellungen | Hostgruppen abrufen | [Umgebungen auflisten](https://developers.adobetarget.com/api/#list-environments) |  |

## Ausnahmen

Wenn Sie eine Ausnahme benötigen, wenden Sie sich an den Kundenerfolgsmanager.

## Hilfe 

Wenden Sie sich an [!DNL Adobe Target Client Care] (tt-support@adobe.com), wenn Sie Fragen haben oder Hilfe beim Übergang von den Classic-APIs zu den [!DNL Target] -APIs auf der [!DNL Adobe Developer Console] benötigen.
