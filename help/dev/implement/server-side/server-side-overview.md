---
keywords: Server-seitig, Server-seitig, API, SDK, Node.js, NodeJS, NodeJS, Recommendations-API, API, APIs, Server-seitig1
description: Erfahren Sie mehr  [!DNL Adobe Target]  die Server-seitigen Bereitstellungs-APIs, SDKs und  [!DNL Target Recommendations] -APIs.
title: Wo erhalte ich Informationen  [!DNL Target]  Server-seitigen Bereitstellungs-APIs und -SDKs?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: 75af30045684b95d5989b0a1f877ba95bb8cd883
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# Serverseitig: [!DNL Target] implementieren

Informationen zu [!DNL Adobe Target] Server-seitigen Bereitstellungs-APIs, SDKs und [!DNL Target Recommendations]-APIs.

>[!NOTE]
>
>Wenn Ihre Implementierung at.js und [!DNL AppMeasurement] Client-seitig verwendet, sollten Sie die unten beschriebenen [!UICONTROL Target Delivery API] und Server-seitigen SDKs verwenden.
>
>Wenn Ihre Implementierung die [!UICONTROL Adobe Experience Platform Web SDK] verwendet, sollten Sie die [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/de/docs/experience-platform/edge-network-server-api/overview){target=_blank} verwenden.

Der folgende Prozess wird in einer Server-seitigen Implementierung von [!DNL Target] ausgeführt:

1. Ein Client-Gerät fordert über Ihren Server ein Erlebnis an.
1. Ihr Server sendet diese Anforderung an [!DNL Target].
1. [!DNL Target] sendet die Antwort zurück an den Server.
1. Ihr Server entscheidet, welches Erlebnis an das Client-Gerät gesendet werden soll, damit es gerendert wird.

Das Erlebnis muss nicht in einem Browser angezeigt werden. Das Erlebnis kann in einer E-Mail oder an einem Kiosk, über einen Sprachassistenten oder über ein anderes nicht visuelles Erlebnis oder nicht browserbasiertes Gerät angezeigt werden. Da sich Ihr Server zwischen dem Client und [!DNL Target] befindet, ist diese Art der Implementierung auch dann optimal, wenn Sie mehr Kontrolle und Sicherheit benötigen oder komplexe Backend-Prozesse haben, die auf Ihrem Server ausgeführt werden sollen.

>[!NOTE]
>
>Ein Erstbesucher kann nur auf der Client-Seite initialisiert werden. Ein Besucher, der zum ersten Mal *, kann* auf der Serverseite initialisiert werden. Dies liegt an der ECID, die vom demdex-Cookie eines Drittanbieters abhängt und daher über Visitor API.js bei einer Implementierung initialisiert werden muss, an der der Browser beteiligt ist.

In den folgenden Abschnitten finden Sie weitere Informationen zu den verschiedenen Server-seitigen APIs und SDKs:

## Server-seitige Bereitstellungs-APIs

Link: [Server-seitige Bereitstellungs-APIs](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Über die [!DNL Target]-Bereitstellungs-API haben Sie folgende Möglichkeiten:

* Bereitstellen von Erlebnissen über Web, einschließlich SPA- und Mobile-Kanälen sowie Nicht-Browser-basierten IoT-Geräten wie vernetzten TVs, Kiosks oder digitalen Bildschirmen in Ladengeschäften.
* Bereitstellen von Erlebnissen von jeder Server-seitigen Plattform oder Anwendung, die HTTP/s-Aufrufe ausführen kann.
* Bereitstellen konsistenter und personalisierter Erlebnisse für einen Besucher, unabhängig davon, über welchen Kanal oder welche Geräte der Besucher mit Ihrem Unternehmen interagiert hat.
* Speichern Sie die Erlebnisse für einen Besucher innerhalb einer Sitzung auf Ihrem Server zwischen, damit mehrere API-Aufrufe vermieden werden können und so eine bessere Leistung erzielt wird.
* Nahtlose Integration mit Adobe Experience Cloud-Produkten wie Adobe Analytics, Adobe Audience Manager (AAM) und dem Experience Cloud-ID-Service von der Serverseite aus.

## Server-seitige SDKs

Die [!DNL Adobe Target] Server-seitige SDK-Dokumentation hilft Ihnen, [!DNL Target] auf Ihren Servern in der Sprache Ihrer Wahl zu implementieren.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Mit den Server-seitigen SDKs von [!DNL Adobe Target] können Sie:

* Ausführen und Ausführen von **Feature**-, **Rollouts**- und **A/B-** mit **Latenz**.
* Bereitstellen von Erlebnissen über **Web**, einschließlich **SPA** und **Mobile-** Kanälen) sowie Nicht-Browser-basierten **Internet of Things (IoT)-Geräten** z. B. einem vernetzten TV, Kiosk oder digitalen Bildschirm im Geschäft.
* Stellen Sie **(ML)-gesteuerte personalisierte Erlebnisse für** bereit, unabhängig davon, über welchen Kanal oder welches Gerät der Benutzer mit Ihrem Unternehmen interagiert hat.
* **Nahtlose Integration mit Adobe Experience Cloud**-Produkten wie **Adobe Analytics**, **Adobe Audience Manager** und dem **Experience Cloud ID-** von Serverseite aus.

Auf der Seite [Erste Schritte](sdk-guides/getting-started/getting-started.md) erfahren Sie, wie Sie einen Anwendungsfall mit einfachem Feature-Flag über [On-Device Decisioning“ ](sdk-guides/on-device-decisioning/overview.md).

Schauen Sie sich unsere [Sample Apps](sdk-guides/sample-apps/sample-apps.md) an, um Spaß zu haben und herumzuspielen!

## [!DNL Target Recommendations]-APIs

Link: [Target Recommendations APIs](https://developers.adobetarget.com/api/recommendations) und [Adobe Recommendations API-Übersicht](../../before-administer/recs-api/overview.md).

Mit den Recommendations-APIs können Sie programmgesteuert mit [!DNL Target] Recommendations-Servern interagieren. Diese APIs können in verschiedene Anwendungs-Stacks integriert werden, um Funktionen durchzuführen, die Sie für gewöhnlich über die [!DNL Target] Benutzeroberfläche ausführen würden.
