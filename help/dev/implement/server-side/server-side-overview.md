---
keywords: serverseitig, serverseitig, api, sdk, node.js, nodejs, node js, recommendations api, api, apis, server side1
description: Informationen zum [!DNL Adobe Target] Server-seitige Bereitstellungs-APIs, SDKs und [!DNL Target Recommendations] APIs.
title: Informationen darüber [!DNL Target] Serverseitige Bereitstellungs-APIs und SDKs?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 14%

---

# Server-seitig: Implementierung [!DNL Target]

Informationen über [!DNL Adobe Target] Server-seitige Bereitstellungs-APIs, SDKs und [!DNL Target Recommendations] APIs.

Der folgende Prozess wird in einer Server-seitigen Implementierung von [!DNL Target] ausgeführt:

1. Ein Client-Gerät fordert über Ihren Server ein Erlebnis an.
1. Ihr Server sendet diese Anforderung an [!DNL Target].
1. [!DNL Target] sendet die Antwort zurück an den Server.
1. Ihr Server entscheidet, welches Erlebnis an das Client-Gerät übermittelt werden soll, damit es gerendert werden kann.

Das Erlebnis muss nicht in einem Browser angezeigt werden. Das Erlebnis kann in einer E-Mail oder an einem Kiosk, über einen Sprachassistenten oder über ein anderes nicht visuelles Erlebnis oder nicht browserbasiertes Gerät angezeigt werden. Da sich Ihr Server zwischen dem Client und [!DNL Target] befindet, ist diese Art der Implementierung auch dann optimal, wenn Sie mehr Kontrolle und Sicherheit benötigen oder komplexe Backend-Prozesse haben, die auf Ihrem Server ausgeführt werden sollen.

>[!NOTE]
>
>Ein erstmaliger Besucher kann nur clientseitig initialisiert werden. Erstmaliger Besucher *cannot* Server-seitig initialisiert werden. Dies liegt an der ECID, die vom Drittanbieter-demdex-Cookie abhängt und daher über die Besucher-API.js in einer Implementierung initialisiert werden muss, in der der Browser involviert ist.

In den folgenden Abschnitten finden Sie weitere Informationen zu den verschiedenen serverseitigen APIs und SDKs:

## Server-seitige Bereitstellungs-APIs

Link: [Server-seitige Bereitstellungs-APIs](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Durch die [!DNL Target] Die Bereitstellungs-API bietet folgende Möglichkeiten:

* Bereitstellung von Erlebnissen über das Internet, einschließlich SPA- und Mobilkanälen sowie Nicht-Browser-basierte IoT-Geräte, wie z. B. angeschlossene TVs, Kiosks oder digitale Bildschirme im Store.
* Stellen Sie Erlebnisse von jeder Server-seitigen Plattform oder Anwendung bereit, die HTTP/s-Aufrufe durchführen kann.
* Bereitstellen konsistenter und personalisierter Erlebnisse für einen Besucher, unabhängig davon, welcher Kanal oder welche Geräte der Besucher für die Interaktion mit Ihrem Unternehmen verwendet hat.
* Zwischenspeichern von Erlebnissen für einen Besucher innerhalb einer Sitzung auf Ihrem Server, sodass mehrere API-Aufrufe vermieden werden können, wodurch eine bessere Leistung erzielt wird.
* Nahtlose Integration mit Adobe Experience Cloud-Produkten wie Adobe Analytics, Adobe Audience Manager (AAM) und dem Experience Cloud-ID-Dienst vom Server aus.

## Server-seitige SDKs

Die [!DNL Adobe Target] Die serverseitige SDK-Dokumentation hilft Ihnen bei der Implementierung von [!DNL Target] auf Ihren Servern in Ihrer gewünschten Sprache.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

bis [!DNL Adobe Target]Server-seitige SDKs verwenden, können Sie:

* Ausführen und Ausführen **Funktionskennzeichnung**, **Rollouts**, und **A/B-Experimente** at **Latenz nahe null**.
* Erlebnisse für alle **Web**, einschließlich **SPA**, und **mobile Kanäle** sowie nicht browserbasierter **Geräte des Internets der Dinge (IoT)** z. B. ein vernetzter TV-, Kiosk- oder In-store-digitaler Bildschirm.
* Versand **Von maschinellem Lernen (ML) gesteuerte personalisierte Erlebnisse** für einen Benutzer, unabhängig davon, welcher Kanal oder welches Gerät der Benutzer mit Ihrem Unternehmen verbunden hat.
* **Nahtlose Integration mit Adobe Experience Cloud** Produkte wie **Adobe Analytics**, **Adobe Audience Manager** und die **Experience Cloud-ID-Dienst** vom Server aus.

Siehe [Erste Schritte](sdk-guides/getting-started/getting-started.md) Seite , auf der Sie erfahren, wie Sie einen einfachen Anwendungsfall beim Kennzeichnen von Funktionen über [on-device decisioning](sdk-guides/on-device-decisioning/overview.md).

Sehen Sie sich unsere [Beispiel-Apps](sdk-guides/sample-apps/sample-apps.md) um Spaß zu haben und herumzuspielen!

## [!DNL Target Recommendations]-APIs

Link: [Target Recommendations-APIs](https://developers.adobetarget.com/api/recommendations) und [Übersicht über die Adobe Recommendations API](../../before-administer/recs-api/overview.md).

Mit den Recommendations-APIs können Sie programmatisch mit [!DNL Target] Recommendations-Server. Diese APIs können in eine Reihe von Anwendungsstacks integriert werden, um Funktionen auszuführen, die Sie normalerweise über die [!DNL Target] -Benutzeroberfläche.
