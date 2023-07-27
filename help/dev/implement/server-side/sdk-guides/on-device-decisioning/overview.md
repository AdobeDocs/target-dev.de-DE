---
keywords: Server-seitig, Server-seitig, SDK, SDK, On-Device, Entscheidungsfindung, auf Gerät, Gerät, Gerät, Nulllatenz, Latenz, nahe null, node.js, Server-seitig3
description: Verwendung von [!UICONTROL [!UICONTROL On-Device Decisioning]] zum Zwischenspeichern Ihrer [!DNL Target] A/B- und MVT-Aktivitäten auf Ihrem Server, um speicherinterne Entscheidungen bei nahezu Nulllatenz durchzuführen.
title: Was ist On-Device Decisioning?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 8%

---

# Übersicht über On-device Decisioning

Die nächste Generation [!DNL Adobe Target] SDK-Angebot jetzt [!UICONTROL on-device decisioning], die Ihnen die Möglichkeit bietet, Ihre A/B- und Erlebnis-Targeting-Kampagnen (XT) auf Ihrem Server zwischenzuspeichern und speicherinterne Entscheidungen zu einer Latenz von nahezu null zu treffen, ohne Netzwerkanforderungen zu blockieren [!DNL Adobe Target]das Edge-Netzwerk.

[!DNL Adobe Target] bietet außerdem die Flexibilität, das relevanteste und aktuellste Erlebnis aus Ihren Experimentierungs- und ML-gestützten Personalisierungskampagnen über einen Live-Server-Aufruf bereitzustellen. Mit anderen Worten: Wenn die Leistung am wichtigsten ist, können Sie [!UICONTROL on-device decisioning], aber wenn das relevanteste und aktuellste Erlebnis benötigt wird, kann stattdessen ein Server-Aufruf durchgeführt werden. Siehe [Verwendung der geräteübergreifenden und Edge-Entscheidung](../../sdk-guides/on-device-decisioning/supported-features.md) , um mehr über Anwendungsfälle zu erfahren, die die Verwendung des einen anstelle des anderen rechtfertigen.

>[!NOTE]
>
>Die Entscheidungsfindung auf dem Gerät ist sowohl für Client- als auch für Server-seitige Implementierungen verfügbar. Dieser Artikel beschreibt [!UICONTROL on-device decisioning] Server-seitig. Informationen über [!UICONTROL on-device decisioning] clientseitig finden Sie in der Dokumentation zur clientseitigen Implementierung . [here](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Wie funktioniert es?

Wenn Sie eine [!DNL Adobe Target] SDK mit [!UICONTROL on-device decisioning] aktiviert ist, *Regelartefakt* wird lokal von dem Akamai CDN heruntergeladen und zwischengespeichert, das Ihrem Server am nächsten ist. Bei einer Anforderung zum Abrufen einer [!DNL Adobe Target] -Erlebnis erfolgt in Ihrer serverseitigen Anwendung. Die Entscheidung darüber, welcher Inhalt im Arbeitsspeicher zurückgegeben werden soll, basiert auf den Metadaten, die im zwischengespeicherten Regel-Artefakt kodiert wurden und all Ihre [!UICONTROL on-device decisioning] A/B- und XT-Aktivitäten.

Das folgende Diagramm zeigt die [!UICONTROL on-device decisioning] Architektur. Klicken Sie auf , um das Bild zu erweitern.

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Architekturdiagramm zu Entscheidungen auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Architekturdiagramm zu Entscheidungen auf dem Gerät"){zoomable=&quot;yes&quot;}

## Was sind die Vorteile?

* **Richten Sie Latenzentscheidungen gegen null ein.** Bucketing und Entscheidungsfindung werden im Arbeitsspeicher und auf dem Gerät ausgeführt, um zu verhindern, dass Netzwerkanforderungen blockiert werden.
* **Verbessern der Anwendungsleistung.** Führen Sie Experimente durch und liefern Sie Ihren Kunden und Benutzern Personalisierung, ohne die Benutzererfahrungen der Endbenutzer zu beeinträchtigen.
* **Verbessern der Google-Site-Qualitätsbewertung.** Da Entscheidungen im Arbeitsspeicher und Server-seitig getroffen werden, verbessern Sie die Google Site Quality-Bewertung Ihres Online-Geschäfts, um es für die Verbraucher leichter zu erkennen.
* **Erfahren Sie mehr über Echtzeitanalysen.** Erhalten Sie Einblicke aus Ihrer Aktivitätsleistung in Echtzeit über [!DNL Adobe Target] oder der A4T-Berichterstellung, sodass Sie Ihre Strategie in kritischen Momenten umdrehen können.

## Unterstützte Funktionen

### Aktivitäten

Die On-Device-Entscheidungsfindung unterstützt die folgenden Aktivitätstypen, die von der [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html):

* [!UICONTROL A/B-Test]
* [!UICONTROL Experience Targeting] (XT)

### Zuordnungsmethode

Die On-Device-Entscheidungsfindung unterstützt die folgende Zuordnungsmethode:

* Manuell

### Zielgruppen-Targeting

Die On-Device-Entscheidungsfindung unterstützt die folgenden Zielgruppenregeln:

| Zielgruppenregel | Gerätebezogene Entscheidungsfindung |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager) | Nein |

## Wie stelle ich meinem Kunden die Verwendung von [!UICONTROL on-device decisioning]?

Die Entscheidung auf dem Gerät ist für alle [!DNL Adobe Target] Kunden, die [!DNL Adobe Target] Server-seitige SDKs. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** im [!DNL Adobe Target] Benutzeroberfläche verwenden und die **[!UICONTROL On-Device Decisioning]** umschalten.

>[!NOTE]
>
>Sie müssen über einen Administrator oder Genehmiger verfügen. *Benutzerrolle* , um die [!UICONTROL On-Device Decisioning] umschalten.

![ALT-Bild](assets/asset-odd-toggle.png)

Nach Aktivierung des Umschalters &quot;On-Device Decisioning&quot;, [!DNL Adobe Target] beginnt mit der Erzeugung und Vermehrung *ruleArtefakte* für Ihren Client.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie den Umschalter aktivieren, bevor Sie die [!DNL Adobe Target] Zu verwendendes SDK [!UICONTROL on-device decisioning]. Die Regelartefakte müssen zunächst die Akamai-CDNs generieren und an sie übertragen, damit [!UICONTROL on-device decisioning] zu arbeiten.

### Alle vorhandenen einschließen [!UICONTROL on-device decisioning] qualifizierte Aktivitäten im Artefaktwechsel

Umschalten **on** wann Sie alles live haben möchten [!DNL Target] Aktivitäten, die für [!UICONTROL on-device decisioning] automatisch in das Artefakt aufgenommen werden.

Umschalten **off** bedeutet, dass Sie alle [!UICONTROL on-device decisioning] -Aktivitäten, damit sie in das generierte Regelartefakt aufgenommen werden.

## Woher weiß ich, dass eine Aktivität [!UICONTROL on-device decisioning] fähig?

Nachdem Sie eine Aktivität erstellt haben, wird die Bezeichnung **[!UICONTROL Entscheidungsmethode]**, der auf der Detailseite der Aktivität angezeigt wird, zeigt an, ob die Aktivität [!UICONTROL on-device decisioning] geeignet.

![ALT-Bild](assets/asset-odd9.png)

Sie können auch alle Aktivitäten sehen, die [!UICONTROL on-device decisioning] auf **[!UICONTROL Tätigkeiten]** Seite durch Hinzufügen der Spalte **[!UICONTROL Entscheidungsmethode]** zur Aktivitätenliste.

![ALT-Bild](assets/asset-odd7.png)

>[!NOTE]
>
>Nach dem Erstellen und Aktivieren einer Aktivität, die [!UICONTROL on-device decisioning] kann es 5-10 Minuten dauern, bis es in das Regelartefakt aufgenommen wird, das generiert und an die Akamai CDN PoPs übertragen wird.

## Wie lauten die Schritte, die ich ausführen muss, um sicherzustellen, dass meine [!UICONTROL on-device decisioning] -Aktivitäten wurden erfolgreich bereitgestellt über [!DNL Adobe Target]Server-seitiges SDK?

1. Zugriff auf [!DNL Adobe Target] Benutzeroberfläche und Navigation **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** um die **[!UICONTROL On-Device Decisioning]** umschalten.
1. Aktivieren Sie die **[!UICONTROL Alle vorhandenen einschließen [!UICONTROL on-device decisioning] qualifizierte Tätigkeiten im Artefakt]** umschalten.
1. Erstellen und aktivieren Sie einen Aktivitätstyp, der von [!UICONTROL on-device decisioning]und stellen Sie sicher, dass die **[!UICONTROL Entscheidungsmethode]** is **[!UICONTROL On-Device Decisioning]** für diese Aktivität.
1. Installieren und initialisieren Sie die [Node.js](../../node-js/overview.md) oder [Java](../../java/overview.md) SDK mit `decisioningMethod = on-device`.
1. Implementierung `getOffers()` oder `getAttributes()` in Ihrem Code, um ein Erlebnis auf dem Gerät abzurufen.
1. Stellen Sie Ihren Code bereit.

Beispiele für die ersten Schritte mit den Schritten 1 bis 3 finden Sie in der [Erste Schritte](../getting-started/getting-started.md) Abschnitt.


## Zusätzliche Ressourcen

### Webinar: Personalisieren und Testen mit Nulllatenz bei geräteinterner Entscheidungsfindung mit [!DNL Adobe Target]

Marketer, Produkteigentümer und Entwickler sind mehr denn je gefordert, die Erlebnisse ihrer Kunden auf Websites, in Apps und überall dort, wo sie mit ihren Kunden in Kontakt treten, zu optimieren. Mehrere Tools mit Datensilos und komplizierten Implementierungen sind unzureichend.

In diesem aufgezeichneten Webinar [!DNL Adobe Target] Produktexperten besprechen, wie sich durch die Verschiebung kritischer Entscheidungen zur Erlebnisoptimierung auf dem Gerät zur lokalen Ausführung mit nahezu Nulllatenz die Türen für aufregende neue Anwendungsfälle öffnen und gleichzeitig die Site-Leistung für Ihre Kunden verbessern lassen.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: Entscheidungsfindung auf dem Gerät

[!DNL Adobe Target] [!UICONTROL on-device decisioning] ermöglicht die Bereitstellung von nahezu null Latenzinhalten.

Dieses 7-minütige Video:

* Beschreibungen [!UICONTROL on-device decisioning], einschließlich des Vergleichs mit anderen Methoden von [!DNL Target] Implementierung
* Veranschaulicht, wie Sie [!UICONTROL on-device decisioning] in Target
* Untersucht eine formularbasierte Composer-Beispielaktivität, die mit JSON-Inhalten konfiguriert wurde
* Zeigt den Beispiel-Node.JS-SDK-Code mit der für [!UICONTROL on-device decisioning]
* Zeigt Ergebnisse in einem Browser an

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Weitere Videos und Tutorials finden Sie im Abschnitt [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=de).

### Adobe Tech Blog - Part 1: Run [!DNL Adobe Target] NodeJS-SDK für Experimentierung und Personalisierung auf Edge-Plattformen (Akamai Edge Workers)

[Klicken Sie hier , um auf den Blogpost zuzugreifen.](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog – Part 2: Führen Sie das [!DNL Adobe Target] NodeJS SDK zum Experimentieren und Personalisieren auf Edge-Plattformen aus (AWS Lambda@Edge)

[Klicken Sie hier , um auf den Blogpost zuzugreifen.](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
