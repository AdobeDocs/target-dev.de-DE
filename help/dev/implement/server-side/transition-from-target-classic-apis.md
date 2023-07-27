---
keywords: api, adobe i/o, classic, adobe developer console
description: Erfahren Sie, wie Sie den Übergang von der [!DNL Adobe Target Classic] APIs für die [!DNL Target] APIs auf der [!DNL Adobe Developer Console].
title: Wie überwinde ich [!DNL Target Classic] APIs für [!DNL Target] APIs auf der [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 34%

---

# Übergang von [!DNL Target Classic] APIs für [!DNL Target] APIs auf der [!DNL Adobe Developer Console]

Informationen für den Übergang von der [!DNL Target Classic] APIs für die [!DNL Target] APIs auf der [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Mit der Stilllegung von [!DNL Adobe Target Classic], die mit Ihren [!DNL Target Classic] -Konto nicht verfügbar gemacht wurde. Dieser Artikel hilft Ihnen beim Übergang Ihrer [!DNL Target Classic] API-basierte Integrationen zum [!DNL Target] APIs, die von der [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

Weitere Informationen finden Sie unter [!DNL Target] APIs, siehe [[!DNL Target] APIs](/help/dev/before-administer/target-api-overview.md). Weitere Informationen finden Sie unter [!DNL Target] SDKs, siehe [[!DNL Target] Serverseitige Implementierung](/help/dev/implement/server-side/server-side-overview.md)

## Terminologie  

| Begriff | Beschreibung |
|--- |--- |
| Klassische API | APIs, die mit Ihren [!DNL Target Classic] -Konto. Diese API-Aufrufe basieren auf einer Benutzername-und-Kennwort-basierten Authentifizierung und verwenden den Hostnamen `testandtarget.omniture.com`. Wenn Ihre API-Aufrufe einen Benutzernamen und ein Kennwort in der Anfrage-URL enthalten, müssen Sie zur [!DNL Adobe Developer Console] APIs. |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | Die [!DNL Adobe Developer Console] ist das Gateway für [!DNL Target] APIs. Diese APIs sind mit Ihren [!DNL Target Standard/Premium] -Konto. Die [!DNL Target] APIs auf der [!DNL Adobe Developer Console] eine [JWT-basierte Authentifizierung](../../before-administer/configure-authentication.md), der Branchenstandard für sichere Enterprise-APIs. |

## Timeline 

Die folgenden APIs wurden bei der Einstellung [!DNL Target Classic] wurde eingestellt:

| Datum | Details |
|--- |--- |
| 17. Oktober 2017 | Alle API-Methoden, die einen Schreibvorgang (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent` und `setCampaignState`) durchführen, wurden beendet.<P>Dies ist dasselbe Datum wie [!DNL Target Classic] Benutzerkonten wurden auf schreibgeschützt gesetzt. |
| 14. November 2017 | Die verbleibenden APIs wurden eingestellt. Dies ist das Datum, an dem der [!DNL Target Classic] Die Benutzeroberfläche wurde eingestellt |

[!DNL Recommendations Classic] APIs wurden von dieser Zeitleiste nicht beeinflusst.

## Äquivalente Methoden 

In der folgenden Tabelle ist das Äquivalent aufgeführt [!DNL Adobe Developer Console] API-Methoden für die klassischen API-Methoden. Die [!DNL Adobe Developer Console] APIs geben JSON zurück, während die klassischen APIs XML zurückgeben.

Die [!DNL Adobe Developer Console] API-Methoden sind mit dem entsprechenden Abschnitt auf der API-Dokumentations-Site verknüpft. Für jede API-Methode wird ein Beispiel angegeben. Sie können auch die [!DNL Target] Admin API Postman-Sammlung mit Beispiel-API-Aufrufen für alle Adobe-API-Methoden auf der [!DNL Adobe Developer Console].

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
|  | Ordnerliste | K. A. | Ordner werden nicht unterstützt in [!DNL Target Standard/Premium] |
| Berichterstellung | Kampagnenleistungsbericht | [AB-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[XT-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | Audit-Bericht | [Audit-Bericht abrufen](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | 1-1-Inhaltsbericht | [AP-Leistungsbericht abrufen](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| Kontoeinstellungen | Hostgruppen abrufen | [Umgebungen auflisten](https://developers.adobetarget.com/api/#list-environments) |  |

## Ausnahmen

Wenn Sie eine Ausnahme benötigen, wenden Sie sich an den Kundenerfolgsmanager.

## Hilfe 

Bitte kontaktieren Sie [!DNL Adobe Target Client Care] (tt-support@adobe.com) wenn Sie Fragen haben oder Hilfe beim Übergang von den Classic-APIs zur benötigen [!DNL Target] APIs auf der [!DNL Adobe Developer Console].
