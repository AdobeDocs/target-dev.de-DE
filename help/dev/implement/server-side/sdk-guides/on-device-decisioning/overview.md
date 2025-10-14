---
keywords: Server-seitig, Server-seitig, SDK, SDKs, geräteintern, Entscheidungsfindung, auf dem Gerät, auf dem Gerät, keine Latenz, Latenz, nahezu null, node.js, Server-seitig3
description: Erfahren Sie, wie Sie mithilfe von [!UICONTROL on-device decisioning] Ihre A/ [!DNL Target] - und MVT-Aktivitäten auf Ihrem Server zwischenspeichern können, um speicherinterne Entscheidungen mit einer Latenz von nahezu null durchzuführen.
title: Was ist On-Device Decisioning?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# Übersicht über On-device Decisioning

Die [!DNL Adobe Target]-SDKs der nächsten Generation bieten jetzt [!UICONTROL on-device decisioning], mit denen Sie Ihre A/B- und Experience Targeting(XT)-Kampagnen auf Ihrem Server zwischenspeichern und speicherinterne Entscheidungen mit einer Latenz von nahezu null durchführen können, ohne Netzwerkanfragen an das Edge Network von [!DNL Adobe Target] zu blockieren.

[!DNL Adobe Target] bietet außerdem die Flexibilität, über einen Live-Server-Aufruf das relevanteste und aktuellste Erlebnis aus Ihren Experiment- und ML-basierten Personalisierungskampagnen bereitzustellen. Mit anderen Worten: Wenn die Leistung am wichtigsten ist, können Sie [!UICONTROL on-device decisioning] nutzen. Wenn jedoch das relevanteste und aktuellste Erlebnis benötigt wird, können Sie stattdessen einen Server-Aufruf ausführen. Siehe [Wann wird die geräteinterne vs. Edge-](../../sdk-guides/on-device-decisioning/supported-features.md) verwendet?, um mehr über Anwendungsfälle zu erfahren, die die Verwendung des einen über den anderen rechtfertigen.

>[!NOTE]
>
>Die geräteinterne Entscheidungsfindung ist sowohl für Client- als auch für Server-seitige Implementierungen verfügbar. In diesem Artikel werden [!UICONTROL on-device decisioning] für Server-seitig beschrieben. Informationen zu Client-seitigen [!UICONTROL on-device decisioning] finden Sie in der Dokumentation zur Client-seitigen Implementierung [hier](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## Wie funktioniert das?

Wenn Sie eine [!DNL Adobe Target] SDK mit aktiviertem [!UICONTROL on-device decisioning] installieren und initialisieren, wird *Regelartefakt* heruntergeladen und lokal von dem Akamai-CDN, das Ihrem Server am nächsten ist, zwischengespeichert. Wenn eine Anfrage zum Abrufen eines [!DNL Adobe Target] Erlebnisses innerhalb Ihrer Server-seitigen Anwendung erfolgt, wird die Entscheidung darüber, welcher Inhalt zurückgegeben werden soll, im Arbeitsspeicher getroffen, basierend auf den Metadaten, die im zwischengespeicherten Regelartefakt codiert sind, das alle Ihre [!UICONTROL on-device decisioning] A/B- und XT-Aktivitäten definiert.

Das folgende Diagramm zeigt die [!UICONTROL on-device decisioning]. Klicken, um das Bild zu erweitern.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Architekturdiagramm für On-Device Decisioning](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "Architekturdiagramm für On-Device Decisioning"){zoomable="yes"}

## Was sind die Vorteile?

* **Entscheidungen mit nahezu null Latenzen treffen.** Bucketing und die Entscheidungsfindung werden im Arbeitsspeicher und auf dem Gerät durchgeführt, um zu vermeiden, dass Netzwerkanfragen blockiert werden.
* **Verbesserung der Anwendungsleistung.** führen Sie Experimente durch und stellen Sie Ihren Kunden und Benutzern Personalisierungen bereit, ohne die Erlebnisse der Endbenutzer zu beeinträchtigen.
* **Verbesserung der Google Site-Qualitätsbewertung.** Da die Entscheidungsfindung im Arbeitsspeicher und auf der Serverseite erfolgt, verbessern Sie den Google-Site-Qualitätsindex Ihres Online-Unternehmens, damit es von Verbrauchern leichter gefunden werden kann.
* **Lernen Sie von der Echtzeit-Analyse.** Gewinnen Sie in Echtzeit über [!DNL Adobe Target]- oder A4T-Berichte Einblicke in Ihre Aktivitätsleistung, sodass Sie Ihre Strategie in kritischen Momenten umstellen können.

## Unterstützte Funktionen

### Aktivitäten

Die geräteinterne Entscheidungsfindung unterstützt die folgenden Aktivitätstypen, die vom ([-basierten Experience Composer) erstellt &#x200B;](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de):

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### Zuordnungsmethode

Die geräteinterne Entscheidungsfindung unterstützt die folgende Zuordnungsmethode:

* Manuell

### Zielgruppen-Targeting

Die geräteinterne Entscheidungsfindung unterstützt die folgenden Zielgruppenregeln:

| Zielgruppenregel | On-device Decisioning |
| --- | --- |
| [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=de) | Ja<P>Bei der Verwendung der geräteinternen Entscheidungsfindung werden die folgenden Geoattribute unterstützt:<ul><li>Land/Region</li><li>Stadt</li><li>Breitengrad</li><li>Längengrad</li></ul> |
| [Netzwerk](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=de) | Nein |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=de) | Nein |
| [Benutzerdefinierte Parameter](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=de) | Ja |
| [Betriebssystem](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=de) | Ja |
| [Seiten der Site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=de) | Ja |
| [Browser](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=de) | Ja |
| [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de) | Nein |
| [Traffic-Quellen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=de) | Nein |
| [Zeitrahmen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=de) | Ja |
| [Experience Cloud-Zielgruppen](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=de) (Zielgruppen aus Adobe Audience Manager, Adobe Analytics und Adobe Experience Manager | Nein |

## Wie stelle ich meinen Client für die Verwendung von [!UICONTROL on-device decisioning] bereit?

Die geräteinterne Entscheidungsfindung ist für alle [!DNL Adobe Target]-Kunden verfügbar, die [!DNL Adobe Target] Server-seitige SDKs verwenden. Um diese Funktion zu aktivieren, navigieren Sie in der [!DNL Adobe Target]-Benutzeroberfläche zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** und aktivieren Sie den Umschalter **[!UICONTROL On-Device Decisioning]** .

>[!NOTE]
>
>Sie müssen über die Rolle Administrator oder Genehmiger *Benutzer) verfügen* um den Umschalter [!UICONTROL On-Device Decisioning] zu aktivieren oder zu deaktivieren.

![ALT-Bild](assets/asset-odd-toggle.png)

Nach der Aktivierung des Umschalters „Geräteinterne Entscheidungsfindung“ beginnt [!DNL Adobe Target] mit der Generierung und Verbreitung *Regelartefakte* für Ihren Client.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie den Umschalter aktivieren, bevor Sie die [!DNL Adobe Target] SDK für die Verwendung von [!UICONTROL on-device decisioning] initialisieren. Die Regelartefakte müssen zunächst generiert und an die Akamai-CDNs weitergegeben werden, damit [!UICONTROL on-device decisioning] funktioniert.

### Alle vorhandenen [!UICONTROL on-device decisioning] qualifizierten Aktivitäten in den Artefakt-Umschalter einschließen

Schalten Sie dieses **ein** wenn alle Ihre Live [!DNL Target]-Aktivitäten, die für [!UICONTROL on-device decisioning] qualifiziert sind, automatisch in das Artefakt aufgenommen werden sollen.

Wenn Sie diesen Umschalter **Aus** lassen, müssen Sie alle [!UICONTROL on-device decisioning] Aktivitäten neu erstellen und aktivieren, damit sie in das generierte Regelartefakt aufgenommen werden.

## Woher weiß ich, dass eine Aktivität [!UICONTROL on-device decisioning] fähig ist?

Nachdem Sie eine Aktivität erstellt haben, gibt ein Titel mit der Bezeichnung **[!UICONTROL Decisioning Method]**, der auf der Detailseite der Aktivität angezeigt wird, an, ob die Aktivität [!UICONTROL on-device decisioning] fähig ist.

![ALT-Bild](assets/asset-odd9.png)

Sie können auch alle Aktivitäten anzeigen, die [!UICONTROL on-device decisioning] auf der Seite **[!UICONTROL Activities]** verfügbar sind, indem Sie die **[!UICONTROL Decisioning Method]** zur Liste der Aktivitäten hinzufügen.

![ALT-Bild](assets/asset-odd7.png)

>[!NOTE]
>
>Nachdem Sie eine Aktivität erstellt und aktiviert haben, die [!UICONTROL on-device decisioning] fähig ist, kann es 20 Minuten dauern, bis sie in das Regelartefakt aufgenommen wird, das generiert und an die Akamai-CDN-Pos weitergegeben wird.

## Wie lautet die Zusammenfassung der Schritte, die ich ausführen muss, um sicherzustellen, dass meine [!UICONTROL on-device decisioning]-Aktivitäten erfolgreich über die Server-seitige SDK von [!DNL Adobe Target] bereitgestellt werden?

1. Rufen Sie die [!DNL Adobe Target]-Benutzeroberfläche auf und navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]** , um den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren.
1. Aktivieren Sie den Umschalter **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** .
1. Erstellen und aktivieren Sie einen Aktivitätstyp, der von [!UICONTROL on-device decisioning] unterstützt wird, und überprüfen Sie, ob der **[!UICONTROL Decisioning Method]** für diese Aktivität **[!UICONTROL On-Device Decisioning]** ist.
1. Installieren und initialisieren Sie [Node.js](../../node-js/overview.md) oder [Java](../../java/overview.md) SDK mit `decisioningMethod = on-device`.
1. Implementieren Sie `getOffers()` oder `getAttributes()` in Ihrem Code, um ein Erlebnis auf dem Gerät abzurufen.
1. Bereitstellen des Codes.

Beispiele, die die ersten Schritte mit den Schritten 1-3 oben veranschaulichen, finden Sie [&#x200B; Abschnitt „Erste Schritte](../getting-started/getting-started.md).


## Zusätzliche Ressourcen

### Webinar: Personalisieren und Testen mit Nulllatenz bei geräteinterner Entscheidungsfindung mit [!DNL Adobe Target]

Marketer, Produkteigentümer und Entwickler sind mehr denn je gefordert, die Erlebnisse ihrer Kunden auf Websites, in Apps und überall dort, wo sie mit ihren Kunden in Kontakt treten, zu optimieren. Verschiedene Tools mit Datensilos und komplizierten Implementierungen sind unzureichend.

In diesem aufgezeichneten Webinar besprechen [!DNL Adobe Target] Produktexperten, wie die Verschiebung kritischer Entscheidungen der Erlebnisoptimierung auf das Gerät durch lokale Ausführung mit nahezu Nulllatenz Türen für aufregende neue Anwendungsfälle öffnet, während sich die Site-Performance Ihrer Kunden gleichzeitig verbessert.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### Tutorial: On-device Decisioning

[!DNL Adobe Target] [!UICONTROL on-device decisioning] ermöglicht die Bereitstellung von Inhalten mit einer Latenz von nahezu null.

Dieses 7-minütige Video:

* Beschreibt [!UICONTROL on-device decisioning], einschließlich der Vergleichbarkeit mit anderen Methoden [!DNL Target] Implementierung
* Veranschaulicht, wie [!UICONTROL on-device decisioning] in Target aktiviert werden
* Untersucht eine beispielhafte formularbasierte Composer-Aktivität, die mit JSON-Inhalten konfiguriert wurde
* Zeigt Beispiel-Code für Node.js-SDK mit der für [!UICONTROL on-device decisioning] erforderlichen Schlüsselkonfiguration an
* Zeigt Ergebnisse in einem Browser an

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

Weitere Videos und Tutorials finden Sie in den [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=de).

### Adobe Tech Blog - Part 1: Führen Sie [!DNL Adobe Target] NodeJS SDK zum Experimentieren und Personalisieren auf Edge-Plattformen aus (Akamai Edge Workers)

[Hier klicken, um den Blogpost aufzurufen](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog – Part 2: Führen Sie das [!DNL Adobe Target] NodeJS SDK zum Experimentieren und Personalisieren auf Edge-Plattformen aus (AWS Lambda@Edge)

[Hier klicken, um den Blogpost aufzurufen](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
