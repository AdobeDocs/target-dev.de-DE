---
keywords: serverseitig, serverseitig, api, sdk, node.js, nodejs, node js, recommendations api, api, apis, server side1
description: Erfahren Sie mehr über die  [!DNL Adobe Target] Server-seitigen Bereitstellungs-APIs, SDKs und [!DNL Target Recommendations] APIs.
title: Wo erhalte ich Informationen zu den serverseitigen Bereitstellungs-APIs und SDKs? [!DNL Target]
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: 75af30045684b95d5989b0a1f877ba95bb8cd883
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# Server-seitig: Implementierung von [!DNL Target]

Informationen zu [!DNL Adobe Target] Server-seitigen Bereitstellungs-APIs, SDKs und [!DNL Target Recommendations] -APIs.

>[!NOTE]
>
>Wenn Ihre Implementierung at.js und [!DNL AppMeasurement] clientseitig verwendet, sollten Sie die unten beschriebenen [!UICONTROL Target Delivery API] und serverseitigen SDKs verwenden.
>
>Wenn Ihre Implementierung den [!UICONTROL Adobe Experience Platform Web SDK] verwendet, sollten Sie den [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank} verwenden.

Der folgende Prozess wird in einer Server-seitigen Implementierung von [!DNL Target] ausgeführt:

1. Ein Client-Gerät fordert über Ihren Server ein Erlebnis an.
1. Ihr Server sendet diese Anforderung an [!DNL Target].
1. [!DNL Target] sendet die Antwort zurück an den Server.
1. Ihr Server entscheidet, welches Erlebnis an das Client-Gerät übermittelt werden soll, damit es gerendert werden kann.

Das Erlebnis muss nicht in einem Browser angezeigt werden. Das Erlebnis kann in einer E-Mail oder an einem Kiosk, über einen Sprachassistenten oder über ein anderes nicht visuelles Erlebnis oder nicht browserbasiertes Gerät angezeigt werden. Da sich Ihr Server zwischen dem Client und [!DNL Target] befindet, ist diese Art der Implementierung auch dann optimal, wenn Sie mehr Kontrolle und Sicherheit benötigen oder komplexe Backend-Prozesse haben, die auf Ihrem Server ausgeführt werden sollen.

>[!NOTE]
>
>Ein erstmaliger Besucher kann nur clientseitig initialisiert werden. Ein erstmaliger Besucher *kann nicht* serverseitig initialisiert werden. Dies liegt an der ECID, die vom Drittanbieter-demdex-Cookie abhängt und daher über die Besucher-API.js in einer Implementierung initialisiert werden muss, in der der Browser involviert ist.

In den folgenden Abschnitten finden Sie weitere Informationen zu den verschiedenen serverseitigen APIs und SDKs:

## Server-seitige Bereitstellungs-APIs

Link: [Server-seitige Bereitstellungs-APIs](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Mit der Bereitstellungs-API [!DNL Target] können Sie:

* Bereitstellung von Erlebnissen über das Internet, einschließlich SPA- und Mobilkanälen sowie Nicht-Browser-basierte IoT-Geräte, wie z. B. angeschlossene TVs, Kiosks oder digitale Bildschirme im Store.
* Stellen Sie Erlebnisse von jeder Server-seitigen Plattform oder Anwendung bereit, die HTTP/s-Aufrufe durchführen kann.
* Bereitstellen konsistenter und personalisierter Erlebnisse für einen Besucher, unabhängig davon, welcher Kanal oder welche Geräte der Besucher für die Interaktion mit Ihrem Unternehmen verwendet hat.
* Zwischenspeichern von Erlebnissen für einen Besucher innerhalb einer Sitzung auf Ihrem Server, sodass mehrere API-Aufrufe vermieden werden können, wodurch eine bessere Leistung erzielt wird.
* Nahtlose Integration mit Adobe Experience Cloud-Produkten wie Adobe Analytics, Adobe Audience Manager (AAM) und dem Experience Cloud ID-Dienst vom Server aus.

## Server-seitige SDKs

Die Dokumentation zum Server-seitigen SDK [!DNL Adobe Target] hilft Ihnen bei der Implementierung von [!DNL Target] auf Ihren Servern in Ihrer bevorzugten Sprache.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Über die Server-seitigen SDKs von [!DNL Adobe Target] können Sie:

* Führen Sie **Feature Flags**, **Rollouts** und **A/B-Experimente** bei **Latenz nahe null** aus und führen Sie sie aus.
* Stellen Sie Erlebnisse für **Web** bereit, einschließlich **SPA** und **Mobile Kanäle** sowie nicht browserbasierter **IoT-Geräte** (z. B. angeschlossene TV-, Kiosk- oder digitale Bildschirme im Geschäft).
* Bereitstellen von durch maschinelles Lernen (ML) gesteuerten personalisierten Erlebnissen **für einen Benutzer, unabhängig davon, welcher Kanal oder welches Gerät der Benutzer für Ihr Unternehmen genutzt hat.**
* **Nahtlose Integration mit Adobe Experience Cloud**-Produkten wie **Adobe Analytics**, **Adobe Audience Manager** und dem **Experience Cloud ID-Dienst** vom Server.

Auf der Seite [Erste Schritte](sdk-guides/getting-started/getting-started.md) erfahren Sie, wie Sie eine einfache Funktion ausführen, die einen Anwendungsfall kennzeichnet, indem Sie [on-device decisioning](sdk-guides/on-device-decisioning/overview.md) verwenden.

Sehen Sie sich unsere [Beispiel-Apps](sdk-guides/sample-apps/sample-apps.md) an, um Spaß zu haben und zu spielen!

## [!DNL Target Recommendations]-APIs

Link: [Target Recommendations APIs](https://developers.adobetarget.com/api/recommendations) und [Adobe Recommendations API Overview](../../before-administer/recs-api/overview.md).

Mit den Recommendations-APIs können Sie programmatisch mit [!DNL Target] Recommendations-Servern interagieren. Diese APIs können in eine Reihe von Anwendungsstacks integriert werden, um Funktionen auszuführen, die Sie normalerweise über die [!DNL Target] -Benutzeroberfläche ausführen würden.
