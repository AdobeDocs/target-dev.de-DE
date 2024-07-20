---
keywords: Server-seitig, Server-seitig, SDK, SDK, On-Device, Entscheidungsfindung, auf Gerät, Gerät, Gerät, Nulllatenz, Latenz, nahe null, node.js, Server-seitig3
description: Erfahren Sie, wie Sie mit [!UICONTROL [!UICONTROL on-device decisioning]] Ihre [!DNL Target] A/B- und MVT-Aktivitäten auf Ihrem Server zwischenspeichern können, um speicherinterne Entscheidungen bei nahezu Nulllatenz durchzuführen.
title: Was ist On-Device Decisioning?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# Übersicht über On-device Decisioning

Die SDK der nächsten Generation [!DNL Adobe Target] bieten jetzt [!UICONTROL on-device decisioning], die Ihnen die Möglichkeit bietet, Ihre A/B- und Erlebnis-Targeting-Kampagnen (XT) auf Ihrem Server zwischenzuspeichern und speicherinterne Entscheidungen bei nahezu null Latenz durchzuführen, ohne Netzwerkanforderungen an das Edge Network von [!DNL Adobe Target] zu blockieren.

[!DNL Adobe Target] bietet außerdem die Flexibilität, das relevanteste und aktuellste Erlebnis aus Ihren Experimentierungs- und ML-gesteuerten Personalisierungskampagnen über einen Live-Server-Aufruf bereitzustellen. Mit anderen Worten: Wenn die Leistung am wichtigsten ist, können Sie [!UICONTROL on-device decisioning] verwenden. Wenn jedoch das relevanteste und aktuellste Erlebnis benötigt wird, kann stattdessen ein Server-Aufruf durchgeführt werden. Informationen zu Anwendungsfällen, die die Verwendung des einen anstelle des anderen rechtfertigen, finden Sie unter [Verwendung von On-Device- oder Edge-Entscheidungen](../../sdk-guides/on-device-decisioning/supported-features.md) .

>[!NOTE]
>
>Die Entscheidungsfindung auf dem Gerät ist sowohl für Client- als auch für Server-seitige Implementierungen verfügbar. In diesem Artikel wird [!UICONTROL on-device decisioning] für serverseitig beschrieben. Informationen zu [!UICONTROL on-device decisioning] für Client-seitig finden Sie in der clientseitigen Implementierungsdokumentation [hier](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Wie funktioniert es?

Wenn Sie ein [!DNL Adobe Target]-SDK installieren und initialisieren, für das [!UICONTROL on-device decisioning] aktiviert ist, wird ein *Regel-Artefakt* vom Akamai-CDN, das Ihrem Server am nächsten ist, heruntergeladen und lokal zwischengespeichert. Wenn in Ihrer serverseitigen Anwendung eine Anforderung zum Abrufen eines [!DNL Adobe Target] -Erlebnisses gestellt wird, wird die Entscheidung darüber, welcher Inhalt zurückgegeben werden soll, im Arbeitsspeicher getroffen, basierend auf den Metadaten, die im zwischengespeicherten Regelartefakt kodiert sind, das alle Ihre [!UICONTROL on-device decisioning] A/B- und XT-Aktivitäten definiert.

Das folgende Diagramm zeigt die [!UICONTROL on-device decisioning] -Architektur. Klicken Sie auf , um das Bild zu erweitern.

(Klicken Sie auf Bild , um die volle Breite zu vergrößern.)

![Architekturdiagramm für Entscheidungen auf dem Gerät](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Architekturdiagramm für Entscheidungen auf dem Gerät"){zoomable="yes"}

## Was sind die Vorteile?

* **Treffen Sie Latenzentscheidungen nahezu null.** Die Erfassung und Entscheidungsfindung erfolgt im Arbeitsspeicher und auf dem Gerät, um zu verhindern, dass Netzwerkanforderungen blockiert werden.
* **Erhöhen Sie die Anwendungsleistung.** Führen Sie Experimente aus und stellen Sie Ihren Kunden und Benutzern Personalisierungen bereit, ohne die Erlebnisse der Endbenutzer zu beeinträchtigen.
* **Verbessern der Google-Site-Qualitätsbewertung.** Da Entscheidungen im Arbeitsspeicher und serverseitig getroffen werden, verbessern Sie die Google Site Quality-Bewertung Ihres Onlinegeschäfts, damit sie von den Verbrauchern leichter gefunden werden können.
* **Erfahren Sie aus Echtzeitanalysen.** Erhalten Sie Einblicke aus Ihrer Aktivitätsleistung in Echtzeit über [!DNL Adobe Target]- oder A4T-Berichte, sodass Sie Ihre Strategie in kritischen Momenten umdrehen können.

## Unterstützte Funktionen

### Aktivitäten

Die Entscheidungsfindung auf dem Gerät unterstützt die folgenden Aktivitätstypen, die vom [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) erstellt wurden:

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Zuordnungsmethode

Die On-Device-Entscheidungsfindung unterstützt die folgende Zuordnungsmethode:

* Manuell

### Zielgruppen-Targeting

Die On-Device-Entscheidungsfindung unterstützt die folgenden Zielgruppenregeln:

| Zielgruppenregel | Gerätebezogene Entscheidungsfindung |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Ja<P>Bei der Verwendung der Entscheidungsfindung auf dem Gerät werden die folgenden Geo-Attribute unterstützt:<ul><li>Land/Region</li><li>Stadt</li><li>Breitengrad</li><li>Längengrad</li></ul> |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Ja |
| [Experience Cloud-Zielgruppen](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager) | Nein |

## Wie stelle ich meinem Client die Verwendung von [!UICONTROL on-device decisioning] bereit?

Die Entscheidungsfindung auf dem Gerät ist für alle [!DNL Adobe Target] -Kunden verfügbar, die [!DNL Adobe Target] Server-seitige SDKs verwenden. Um diese Funktion zu aktivieren, navigieren Sie in der Benutzeroberfläche von [!DNL Adobe Target] zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

>[!NOTE]
>
>Sie müssen über die Benutzerrolle &quot;Admin&quot;oder &quot;Genehmiger&quot;*Benutzer* verfügen, um den Umschalter [!UICONTROL On-Device Decisioning] zu aktivieren oder zu deaktivieren.

![alt image](assets/asset-odd-toggle.png)

Nachdem Sie den Umschalter &quot;on-Device Decisioning&quot;aktiviert haben, beginnt [!DNL Adobe Target] mit der Generierung und Verbreitung von *Regel-Artefakten* für Ihren Client.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie den Umschalter aktivieren, bevor Sie das [!DNL Adobe Target] SDK für die Verwendung von [!UICONTROL on-device decisioning] initialisieren. Die Regelartefakte müssen zuerst generiert und an die Akamai-CDNs übertragen werden, damit [!UICONTROL on-device decisioning] funktioniert.

### Alle vorhandenen [!UICONTROL on-device decisioning] qualifizierten Aktivitäten in den Artefakt-Umschalter einschließen

Schalten Sie diese **auf** um, wenn alle Ihre Live-[!DNL Target]-Aktivitäten, die für [!UICONTROL on-device decisioning] qualifiziert sind, automatisch in das Artefakt einbezogen werden sollen.

Wenn Sie diesen Umschalter **aus** lassen, müssen Sie alle [!UICONTROL on-device decisioning] -Aktivitäten neu erstellen und aktivieren, damit sie in das generierte Regelartefakt aufgenommen werden.

## Woher weiß ich, dass eine Aktivität [!UICONTROL on-device decisioning] fähig ist?

Nachdem Sie eine Aktivität erstellt haben, zeigt eine Bezeichnung mit dem Namen &quot;**[!UICONTROL Decisioning Method]**&quot;, die auf der Detailseite der Aktivität angezeigt wird, ob die Aktivität [!UICONTROL on-device decisioning] fähig ist.

![alt image](assets/asset-odd9.png)

Sie können auch alle Aktivitäten sehen, die [!UICONTROL on-device decisioning] für die Seite **[!UICONTROL Activities]** geeignet sind, indem Sie die Spalte **[!UICONTROL Decisioning Method]** zur Aktivitätenliste hinzufügen.

![alt image](assets/asset-odd7.png)

>[!NOTE]
>
>Nach dem Erstellen und Aktivieren einer Aktivität, die [!UICONTROL on-device decisioning] fähig ist, kann es 20 Minuten dauern, bis sie im Regelartefakt enthalten ist, das generiert und an die Akamai CDN PoPs weitergeleitet wird.

## Wie lauten die Schritte, die ich ausführen muss, um sicherzustellen, dass meine [!UICONTROL on-device decisioning] -Aktivitäten erfolgreich über das serverseitige SDK von [!DNL Adobe Target] bereitgestellt werden?

1. Rufen Sie die [!DNL Adobe Target] -Benutzeroberfläche auf und navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** , um den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren.
1. Aktivieren Sie den Umschalter **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** .
1. Erstellen und aktivieren Sie einen Aktivitätstyp, der von [!UICONTROL on-device decisioning] unterstützt wird, und stellen Sie sicher, dass der **[!UICONTROL Decisioning Method]** für diese Aktivität **[!UICONTROL On-Device Decisioning]** ist.
1. Installieren und initialisieren Sie das SDK [Node.js](../../node-js/overview.md) oder [Java](../../java/overview.md) mit `decisioningMethod = on-device`.
1. Implementieren Sie `getOffers()` oder `getAttributes()` in Ihren Code, um ein Erlebnis auf dem Gerät abzurufen.
1. Stellen Sie Ihren Code bereit.

Beispiele für die ersten Schritte mit den Schritten 1 bis 3 oben finden Sie im Abschnitt [Erste Schritte](../getting-started/getting-started.md) .


## Zusätzliche Ressourcen

### Webinar: Personalisieren und Testen mit Nulllatenz bei geräteinterner Entscheidungsfindung mit [!DNL Adobe Target]

Marketer, Produkteigentümer und Entwickler sind mehr denn je gefordert, die Erlebnisse ihrer Kunden auf Websites, in Apps und überall dort, wo sie mit ihren Kunden in Kontakt treten, zu optimieren. Mehrere Tools mit Datensilos und komplizierten Implementierungen sind unzureichend.

In diesem aufgezeichneten Webinar besprechen [!DNL Adobe Target] Produktexperten, wie bewegte Entscheidungen zur Optimierung kritischer Erlebnisse auf dem Gerät zur lokalen Ausführung mit nahezu Nulllatenz Türen zu aufregenden neuen Anwendungsfällen öffnen und gleichzeitig die Site-Leistung für Ihre Kunden verbessern können.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: Entscheidungsfindung auf dem Gerät

[!DNL Adobe Target] [!UICONTROL on-device decisioning] ermöglicht die Bereitstellung von nahezu null Latenzinhalten.

Dieses 7-minütige Video:

* Beschreibt [!UICONTROL on-device decisioning], einschließlich dessen, wie er mit anderen Methoden der Implementierung von [!DNL Target] verglichen wird
* Veranschaulicht, wie [!UICONTROL on-device decisioning] in Target aktiviert wird
* Untersucht eine formularbasierte Composer-Beispielaktivität, die mit JSON-Inhalten konfiguriert wurde
* Zeigt den Beispiel-Node.JS-SDK-Code mit der für [!UICONTROL on-device decisioning] erforderlichen Schlüsselkonfiguration an
* Zeigt Ergebnisse in einem Browser an

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Weitere Videos und Tutorials finden Sie in den [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=de).

### Adobe Tech Blog - Part 1: Run [!DNL Adobe Target] NodeJS SDK for experimentation and personalization on edge platforms (Akamai Edge Workers)

[Klicken Sie hier, um auf den Blogpost zuzugreifen](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog – Part 2: Führen Sie das [!DNL Adobe Target] NodeJS SDK zum Experimentieren und Personalisieren auf Edge-Plattformen aus (AWS Lambda@Edge)

[Klicken Sie hier, um auf den Blogpost zuzugreifen](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
