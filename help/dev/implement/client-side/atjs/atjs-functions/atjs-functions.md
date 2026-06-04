---
keywords: at.js, Funktionen, JavaScript-Bibliothek
description: Eine Liste der Funktionen anzeigen, die mit den Versionen 1.x und 2.x der at.js-JavaScript-Bibliothek in [!DNL Adobe Target] verwendet werden können.
title: Welche Funktionen kann ich mit at.js verwenden?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
TQID: https://experienceleague.adobe.com/7uABK1rDaMpA7a0skEo3g1KxTnoc-gif-uHMkMnE8QE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 38%

---

# „at.js“-Funktionen

Liste der Funktionen, die mit der [!DNL Adobe Target] at.js-JavaScript-Bibliothek verwendet werden können. Klicken Sie in der Spalte „Funktion“ auf die Links, um weitere Informationen und Beispiele zu erhalten.

| Funktion | Details |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | Diese Funktion löst eine Anfrage aus, um ein [!DNL Target] Angebot abzurufen. Verwenden Sie sie mit `adobe.target.applyOffer()`, um die Antwort zu verarbeiten, oder verwenden Sie Ihre eigene Methode für die Verarbeitung von „success“. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | Mit dieser Funktion können Sie mehrere Angebote abrufen, indem Sie mehrere Mboxes übergeben. Darüber hinaus können mehrere Angebote für alle Ansichten in aktiven Aktivitäten abgerufen werden.<P>**Hinweis:** Diese Funktion wurde mit at.js 2.x eingeführt. Diese Funktion ist nicht verfügbar für at.js-Version 1.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | Diese Funktion dient zur Anwendung der Antwortinhalte. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | Mit dieser Funktion können Sie mehr als ein Angebot anwenden, das von [!UICONTROL adobe.target.getOffers() abgerufen ].<P>**Hinweis:** Diese Funktion wurde mit at.js 2.x eingeführt. Diese Funktion ist nicht verfügbar für at.js-Version 1.*x*. |
| [[!UICONTROL adobe.target.triggerView (ViewName, Optionen)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | Diese Funktion kann immer aufgerufen werden, wenn eine neue Seite geladen wird oder wenn eine Komponente auf einer Seite erneut wiedergegeben wird.<P> Diese Funktion sollte für Single Page Applications (SPAs) implementiert werden, damit der [!UICONTROL Visual Experience Composer] (VEC) zum Erstellen von [!UICONTROL A/B-Test]- und [!UICONTROL Experience Targeting] (XT)-Aktivitäten verwendet werden kann. |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | Diese Funktion löst eine Anforderung zum Melden von Benutzeraktionen aus (wie beispielsweise Klicks und Konversionen). Sie übermittelt keine Aktivitäten in der Antwort. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | Führt eine Anforderung aus und wendet das Angebot auf den nächsten DIV-Bereich mit dem Klassennamen „mboxDefault“ an.<P>**Hinweis:** Diese Funktion ist nur für at.js-Versionen 1.*x* verfügbar. Diese Funktion wird seit der Veröffentlichung von at.js 2.x nicht mehr unterstützt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird. |
| [[!UICONTROL mboxDefine(options)] und [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | Mbox definieren und aktualisieren<P>**Hinweis:** Diese Funktion ist nur für at.js-Versionen 1.*x* verfügbar. Diese Funktion wird seit der Veröffentlichung von at.js 2.x nicht mehr unterstützt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | Sie können Einstellungen in der at.js-Bibliothek mithilfe von `[!UICONTROL targetGlobalSettings()]` überschreiben, anstatt sie in der [!DNL Target Standard/Premium]-Benutzeroberfläche oder durch Verwendung von REST-APIs zu konfigurieren.<ul><li>Datenanbieter: Mit dieser Einstellung können Kunden Daten von Drittdatenanbietern sammeln, beispielsweise Demandbase, BlueKai und benutzerspezifischen Services, und die Daten an Target als Mbox-Parameter in der globalen Mbox-Anfrage weitergeben.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | Mit dieser Methode können Sie Parameter von außerhalb des Anforderungscodes an die globale Mbox anfügen. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | Mit dieser Methode können Sie Parameter von außerhalb des Anforderungscodes an alle Mboxes anfügen. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | Stellt eine Standardart zur Registrierung bestimmter Erweiterungen dar.<P>**Hinweis:** Diese Funktion ist nur für at.js-Versionen 1.*x* verfügbar. Diese Funktion wird seit der Veröffentlichung von at.js 2.x nicht mehr unterstützt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird. |
| [[!UICONTROL Benutzerdefinierte at.js-Ereignisse]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | Benutzerdefinierte at.js-Ereignisse teilen Ihnen mit, wenn eine Mbox-Anforderung oder ein Angebot erfolgreich oder fehlgeschlagen ist. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | Diese Funktion sendet eine Benachrichtigung an [!DNL Target] Edge, wenn ein Erlebnis ohne Verwendung von `[!UICONTROL adobe.target.applyOffer()]` oder `[!UICONTROL adobe.target.applyOffers()]` gerendert wird.<P>**Hinweis**: Diese Funktion wurde in at.js 2.1.0 eingeführt und wird für alle Versionen über 2.1.0 verfügbar sein. |
