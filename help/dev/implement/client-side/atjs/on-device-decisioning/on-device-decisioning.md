---
keywords: Implementierung, JavaScript-Bibliothek, js, atjs, Entscheidungsfindung auf dem Gerät, Entscheidungsfindung auf dem Gerät, at.js, auf dem Gerät, Implementierung0
description: Erfahren Sie, wie Sie [!UICONTROL on-device decisioning] mit der at.js-Bibliothek durchführen
title: Wie funktioniert die geräteinterne Entscheidungsfindung mit der at.js-JavaScript-Bibliothek?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 4%

---

# [!UICONTROL On-device decisioning] für at.js

Ab Version 2.5.0 bietet at.js [!UICONTROL on-device decisioning]. [!UICONTROL On-device decisioning] können Sie Ihre [A/B-Test](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)- und [Experience Targeting](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)-Aktivitäten (XT) im Browser zwischenspeichern, um speicherinterne Entscheidungen durchzuführen, ohne eine Netzwerkanfrage an das [!DNL Adobe Target]-Edge Network zu blockieren.

>[!NOTE]
>
>[!UICONTROL On-device decisioning] ist sowohl für Client- als auch für Server-seitige Implementierungen verfügbar. In diesem Artikel werden [!UICONTROL on-device decisioning] für die Client-Seite beschrieben. Informationen zu [!UICONTROL on-device decisioning] für Server-seitig finden Sie in der Dokumentation zur Server-seitigen Implementierung [hier](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] bietet außerdem die Flexibilität, über einen Live-Server-Aufruf das relevanteste und aktuellste Erlebnis aus Ihren experimentellen und auf maschinellem Lernen (ML-gesteuert) basierenden Personalisierungsaktivitäten bereitzustellen. Mit anderen Worten: Wenn die Leistung am wichtigsten ist, können Sie [!UICONTROL on-device decisioning] verwenden. Wenn jedoch das relevanteste, aktuellste und ML-gesteuerte Erlebnis benötigt wird, kann stattdessen ein Server-Aufruf durchgeführt werden.

## Was sind die Vorteile von [!UICONTROL on-device decisioning]?

Zu den Vorteilen von [!UICONTROL on-device decisioning] gehören:

* **Schnelle Entscheidungen und Erlebnisse liefern** Bucketing und die Entscheidungsfindung werden im Arbeitsspeicher und im Browser durchgeführt, um das Blockieren von Netzwerkanfragen zu vermeiden.
* **Verbesserung der Anwendungsleistung.** führen Sie Experimente durch und stellen Sie Ihren Kunden und Benutzern Personalisierungen bereit, ohne die Erlebnisse der Endbenutzer zu beeinträchtigen.
* **Verbesserung der Google Site-Qualitätsbewertung.** Da die Entscheidungsfindung im Arbeitsspeicher stattfindet, verbessern Sie den Google-Site-Qualitätsindex Ihres Online-Unternehmens, damit es von Verbrauchern besser gefunden werden kann.
* **Lernen Sie von der Echtzeit-Analyse.** Gewinnen Sie Erkenntnisse aus Ihrer Aktivitätsleistung in Echtzeit über die Berichterstellung [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T). Mit A4T können Sie Ihre Strategie in kritischen Momenten umstellen.

## Unterstützte Funktionen

Die [!DNL Adobe Target] JS-SDK bietet Kundinnen und Kunden die Flexibilität, bei Entscheidungen zwischen Leistung und Aktualität der Daten zu wählen. Mit anderen Worten: Wenn die Bereitstellung der relevantesten und ansprechendsten personalisierten Inhalte über maschinelles Lernen für Sie am wichtigsten ist, sollte ein Live-Server-Aufruf erfolgen. Wenn die Leistung jedoch kritischer ist, sollte eine Entscheidung auf dem Gerät und im Arbeitsspeicher getroffen werden. Informationen zum [!UICONTROL on-device decisioning] finden Sie in der Liste der unterstützten Funktionen:

* Aktivitätstypen 
* Zielgruppen-Targeting
* Zuordnungsmethode

Weitere Informationen finden Sie unter [Unterstützte Funktionen für [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## Wie funktioniert [!UICONTROL on-device decisioning]?

Wenn Sie at.js mit aktiviertem [!UICONTROL on-device decisioning] bereitstellen und initialisieren, wird ein [Regelartefakt](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) das Ihre [!UICONTROL on-device decisioning] für A/B- und XT-Aktivitäten, Zielgruppen und Assets enthält, vom nächstgelegenen Akamai-CDN für Ihren Besucher heruntergeladen und lokal im Browser Ihres Besuchers zwischengespeichert. Wenn at.js den Abruf eines Erlebnisses anfordert, wird die Entscheidung, welches Erlebnis zurückgegeben werden soll, basierend auf den im zwischengespeicherten Regelartefakt codierten Metadaten speicherintern getroffen.

## Entscheidungsmethode

Mit [!UICONTROL on-device decisioning] führt [!DNL Target] eine neue Einstellung namens Entscheidungsmethode ein. Die Einstellung Entscheidungsmethode bestimmt, wie at.js Ihre Erlebnisse bereitstellt. Die Entscheidungsmethode hat drei Werte:

* Nur Server-seitig
* Nur auf dem Gerät
* Hybrid

### Nur Server-seitig

Nur Server-seitig ist die standardmäßige Entscheidungsmethode, die vorkonfiguriert ist, wenn at.js 2.5.0+ implementiert und in Ihren Web-Eigenschaften bereitgestellt wird.

Die Verwendung von Nur Server-seitig als Standardkonfiguration bedeutet, dass alle Entscheidungen im [!DNL Target] Edge Network getroffen werden, was einen blockierenden Server-Aufruf beinhaltet. Dieser Ansatz kann zu einer inkrementellen Latenz führen, bietet aber auch erhebliche Vorteile, z. B. die Möglichkeit, die maschinellen Lernfunktionen von [!DNL Target] anzuwenden, zu denen die Aktivitäten [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) und [Automatisches Targeting](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) gehören.

Darüber hinaus kann die Verbesserung Ihrer personalisierten Erlebnisse mithilfe des Benutzerprofils von [!DNL Target], das sitzungs- und kanalübergreifend beibehalten wird, leistungsstarke Ergebnisse für Ihr Unternehmen liefern.

Schließlich erlaubt Ihnen Nur Server-seitig , die Adobe Experience Cloud zu verwenden und Zielgruppen anzupassen, die über Audience Manager- und Adobe Analytics-Segmente angesprochen werden können.

Das folgende Diagramm veranschaulicht die Interaktion zwischen dem Besucher, dem Browser, at.js 2.5.0+ und dem [!DNL Adobe Target] Edge-Netzwerk. Dieses Flussdiagramm erfasst neue Besucher und wiederkehrende Besucher.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Nur Server-seitiges Flussdiagramm](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png " Nur Server-seitiges Flussdiagramm"){zoomable="yes"}

Die folgende Liste entspricht den Zahlen im Diagramm:

| Schritt | Beschreibung |
| --- | --- |
| 1 | Die Experience Cloud-Besucher-ID wird vom [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?) abgerufen. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<br />   Die at.js-Bibliothek kann auch asynchron geladen werden, wobei ein optionales pre-hiding-Snippet auf der Seite implementiert ist. |
| 3 | Die at.js-Bibliothek blendet den Hauptteil aus, um Flackern zu verhindern. |
| 4 | Es wird eine Seitenladeanfrage gestellt, die alle konfigurierten Parameter wie (ECID, Kunden-ID, benutzerdefinierte Parameter, Benutzerprofil usw.) enthält. |
| 5 | Profilskripte werden ausgeführt und dann in den Profilspeicher eingespeist.<br />Der Profilspeicher fordert qualifizierte Zielgruppen aus der Zielgruppenbibliothek an (z. B. aus Adobe Analytics, Adobe Audience Manager freigegebene Zielgruppen).<br />Kundenattribute werden in einem Batch-Prozess an den Profilspeicher übermittelt. |
| 6 | Der Profilspeicher wird für die Zielgruppen-Qualifizierung und Bucketing zum Filtern von Aktivitäten verwendet. |
| 7 | Der resultierende Inhalt wird ausgewählt, nachdem das Erlebnis aus Live-[!DNL Target]-Aktivitäten ermittelt wurde. |
| 8 | Die at.js-Bibliothek blendet die entsprechenden Elemente auf der Seite aus, die mit dem Erlebnis verknüpft sind, das gerendert werden muss. |
| 9 | Die at.js-Bibliothek zeigt den Hauptteil an, sodass der Rest der Seite geladen werden kann, damit der Besucher ihn anzeigen kann. |
| 10 | Die at.js-Bibliothek bearbeitet das DOM, um das Erlebnis aus dem [!DNL Target]-Edge Network zu rendern. |
| 11 | Das Erlebnis wird für den Besucher dargestellt. |
| 12 | Die gesamte Webseite wird geladen. |
| 13 | Analytics-Daten werden an Datenerfassungsserver übermittelt. |
| 14 | Zielgruppendaten werden über die SDID mit den Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet. Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

### Nur auf dem Gerät

Nur auf dem Gerät ist die Entscheidungsmethode, die in at.js 2.5.0 oder höher festgelegt werden muss, wenn [!UICONTROL on-device decisioning] nur auf Ihren Web-Seiten verwendet werden soll.

[!UICONTROL On-device decisioning] können Ihre Erlebnisse und Personalisierungsaktivitäten schnell bereitstellen, da die Entscheidungen aus einem zwischengespeicherten Regelartefakt getroffen werden, das all Ihre Aktivitäten enthält, die für [!UICONTROL on-device decisioning] qualifiziert sind.

Weitere Informationen dazu, welche Aktivitäten für [!UICONTROL on-device decisioning] qualifiziert sind, finden Sie unter [Unterstützte Funktionen in [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

Diese Entscheidungsmethode sollte nur verwendet werden, wenn die Leistung auf allen Seiten, für die Entscheidungen von Target erforderlich sind, äußerst kritisch ist. Beachten Sie außerdem, dass bei Auswahl dieser Entscheidungsmethode Ihre [!DNL Target] Aktivitäten, die nicht für [!UICONTROL on-device decisioning] qualifiziert sind, nicht bereitgestellt bzw. ausgeführt werden. Die at.js-Bibliothek 2.5.0+ ist so konfiguriert, dass nur nach dem zwischengespeicherten Regelartefakt gesucht wird, um Entscheidungen zu treffen.

Das folgende Diagramm veranschaulicht die Interaktion zwischen Ihrem Besucher, dem Browser, at.js 2.5.0+ und dem Akamai-CDN. Das Akamai-CDN speichert das Regelartefakt für den ersten Besuch des Besuchers im Zwischenspeicher. Für den ersten Seitenbesuch eines neuen Besuchers muss das JSON-Regelartefakt vom Akamai-CDN heruntergeladen werden, damit es lokal im Browser des Besuchers zwischengespeichert wird. Nachdem das JSON-Regelartefakt heruntergeladen wurde, wird die Entscheidung sofort ohne einen blockierenden Netzwerkaufruf getroffen. Das folgende Flussdiagramm erfasst neue Besucher.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Flussdiagramm nur auf dem Gerät](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "Flussdiagramm nur auf dem Gerät"){zoomable="yes"}

Die folgende Liste entspricht den Zahlen im Diagramm:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-Server qualifizieren alle Ihre Aktivitäten, die für die [!UICONTROL on-device decisioning] infrage kommen, generieren das JSON-Regelartefakt und übertragen es an das Akamai-CDN. Ihre Aktivitäten werden kontinuierlich auf Aktualisierungen überwacht, um ein neues JSON-Regelartefakt auszugeben, das an das Akamai-CDN weitergegeben wird.

| Schritt | Beschreibung |
| --- | --- |
| 1 | Die Experience Cloud-Besucher-ID wird vom [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) abgerufen. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<br />Die at.js-Bibliothek kann auch asynchron geladen werden, wobei ein optionales pre-hiding-Snippet auf der Seite implementiert ist. |
| 3 | Die at.js-Bibliothek blendet den Hauptteil aus, um Flackern zu verhindern. |
| 4 | Die at.js-Bibliothek stellt eine Anfrage, um das JSON-Regelartefakt vom nächsten Akamai-CDN für den Besucher abzurufen. |
| 5 | Das Akamai-CDN antwortet mit dem JSON-Regel-Artefakt. |
| 6 | Das JSON-Regelartefakt wird lokal im Browser des Besuchers zwischengespeichert. |
| 7 | Die at.js-Bibliothek interpretiert das JSON-Regelartefakt und führt die Entscheidung zum Abrufen des Erlebnisses aus und blendet die getesteten Elemente aus. |
| 8 | Die at.js-Bibliothek zeigt den Hauptteil an, sodass der Rest der Seite geladen werden kann, damit der Besucher ihn anzeigen kann. |
| 9 | Die at.js-Bibliothek bearbeitet das DOM, um das Erlebnis aus dem zwischengespeicherten JSON-Regel-Artefakt zu rendern. |
| 10 | Das Erlebnis wird für den Besucher dargestellt. |
| 11 | Die gesamte Webseite wird geladen. |
| 12 | Analytics-Daten werden an Datenerfassungs-Server gesendet. Zielgruppendaten werden über die SDID mit den Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet. Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

Das folgende Diagramm veranschaulicht die Interaktion zwischen Ihrem Besucher, dem Browser, at.js 2.5.0+ und dem zwischengespeicherten JSON-Regel-Artefakt für den nachfolgenden Seitenaufruf oder wiederkehrenden Besuch des Besuchers. Da das JSON-Regelartefakt bereits zwischengespeichert und im Browser verfügbar ist, wird die Entscheidung sofort ohne einen blockierenden Netzwerkaufruf getroffen. Dieses Flussdiagramm erfasst die nachfolgende Seitennavigation oder wiederkehrende Besucher.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Flussdiagramm nur auf dem Gerät für nachfolgende Seitennavigation und Wiederholungsbesuche](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png " Flussdiagramm nur auf dem Gerät für nachfolgende Seitennavigation und Wiederholungsbesuche"){zoomable="yes"}

Die folgende Liste entspricht den Zahlen im Diagramm:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-Server qualifizieren alle Ihre Aktivitäten, die für die [!UICONTROL on-device decisioning] infrage kommen, generieren das JSON-Regelartefakt und übertragen es an das Akamai-CDN. Ihre Aktivitäten werden kontinuierlich auf Aktualisierungen überwacht, um ein neues JSON-Regelartefakt auszugeben, das an das Akamai-CDN weitergegeben wird.

| Schritt | Beschreibung |
| --- | --- |
| 1 | Die Experience Cloud-Besucher-ID wird vom [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) abgerufen. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<br />Die at.js-Bibliothek kann auch asynchron geladen werden, wobei ein optionales pre-hiding-Snippet auf der Seite implementiert ist. |
| 3 | Die at.js-Bibliothek blendet den Hauptteil aus, um Flackern zu verhindern. |
| 4 | Die at.js-Bibliothek interpretiert das JSON-Regelartefakt und führt die Entscheidung im Speicher aus, um das Erlebnis abzurufen. |
| 5 | Die getesteten Elemente sind ausgeblendet. |
| 6 | Die at.js-Bibliothek zeigt den Hauptteil an, sodass der Rest der Seite geladen werden kann, damit der Besucher ihn anzeigen kann. |
| 7 | Die at.js-Bibliothek bearbeitet das DOM, um das Erlebnis aus dem zwischengespeicherten JSON-Regel-Artefakt zu rendern. |
| 8 | Das Erlebnis wird für den Besucher dargestellt. |
| 9 | Die gesamte Webseite wird geladen. |
| 10 | Analytics-Daten werden an Datenerfassungs-Server gesendet. Zielgruppendaten werden über die SDID mit den Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet. Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

### Hybrid

Hybrid ist die Entscheidungsmethode, die in at.js 2.5.0+ festgelegt werden muss, wenn sowohl [!UICONTROL on-device decisioning] als auch Aktivitäten, die einen Netzwerkaufruf an das [!DNL Adobe Target] Edge-Netzwerk erfordern, ausgeführt werden müssen.

Wenn Sie sowohl [!UICONTROL on-device decisioning] als auch Server-seitige Aktivitäten verwalten, kann es bei der Bereitstellung von [!DNL Target] auf Ihren Seiten etwas kompliziert und mühsam werden. Bei „Hybrid“ als Entscheidungsmethode weiß [!DNL Target], wann ein Server-Aufruf an das [!DNL Adobe Target] Edge-Netzwerk für Aktivitäten durchgeführt werden muss, für die eine Server-seitige Ausführung erforderlich ist, und wann nur Entscheidungen auf dem Gerät ausgeführt werden sollen.

Das JSON-Regelartefakt enthält Metadaten, die at.js darüber informieren, ob eine Mbox eine Server-seitige Aktivität ausführt oder eine [!UICONTROL on-device decisioning] Aktivität aufweist. Diese Entscheidungsmethode stellt sicher, dass Aktivitäten, die Sie schnell bereitstellen möchten, über [!UICONTROL on-device decisioning] durchgeführt werden und für Aktivitäten, die eine leistungsfähigere ML-gesteuerte Personalisierung erfordern, diese Aktivitäten über das [!DNL Adobe Target] Edge-Netzwerk erfolgen.

Die folgende Abbildung zeigt die Interaktion zwischen dem Besucher, dem Browser, at.js 2.5.0+, dem Akamai-CDN und dem [!DNL Adobe Target] Edge Network für einen neuen Besucher, der Ihre Seite zum ersten Mal besucht. Aus diesem Diagramm geht hervor, dass das JSON-Regelartefakt asynchron heruntergeladen wird, während die Entscheidungen über das [!DNL Adobe Target] Edge-Netzwerk getroffen werden.

Dadurch wird sichergestellt, dass die Größe des Artefakts, die viele Aktivitäten enthalten kann, die Latenz der Entscheidung nicht negativ beeinflusst. Das synchrone Herunterladen des JSON-Regelartefakts und das anschließende Treffen der Entscheidung können sich auch negativ auf die Latenz auswirken und inkonsistent sein. Daher ist die hybride Entscheidungsmethode eine Best-Practice-Empfehlung, für einen neuen Besucher immer einen Server-seitigen Aufruf für die Entscheidung durchzuführen, da das JSON-Regelartefakt parallel zwischengespeichert wird. Bei allen nachfolgenden Seitenbesuchen und wiederkehrenden Besuchen werden die Entscheidungen aus dem Cache und im Arbeitsspeicher über das JSON-Regelartefakt getroffen.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Hybrides Flussdiagramm für ein erstmaliges Besucher-](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "-Hybrides Flussdiagramm für einen erstmaligen Besucher"){zoomable="yes"}

Die folgende Liste entspricht den Zahlen im Diagramm:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-Server qualifizieren alle Ihre Aktivitäten, die für die [!UICONTROL on-device decisioning] infrage kommen, generieren das JSON-Regelartefakt und übertragen es an das Akamai-CDN. Ihre Aktivitäten werden kontinuierlich auf Aktualisierungen überwacht, um ein neues JSON-Regelartefakt auszugeben, das an das Akamai-CDN weitergegeben wird.

| Schritt | Beschreibung |
| --- | --- |
| 1 | Die Experience Cloud-Besucher-ID wird vom [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) abgerufen. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<br />Die at.js-Bibliothek kann auch asynchron geladen werden, wobei ein optionales pre-hiding-Snippet auf der Seite implementiert ist. |
| 3 | Die at.js-Bibliothek blendet den Hauptteil aus, um Flackern zu verhindern. |
| 4 | Eine Seitenladeanfrage wird an das [!DNL Adobe Target]-Edge Network gesendet, einschließlich aller konfigurierten Parameter wie (ECID, Kunden-ID, benutzerdefinierte Parameter, Benutzerprofil usw.) |
| 5 | Parallel dazu fordert at.js den Besucher auf, das JSON-Regelartefakt vom nächsten Akamai-CDN abzurufen. |
| 6 | ([!DNL Adobe Target] Edge Network) Profilskripte werden ausgeführt und dann in den Profilspeicher eingespeist. Der Profilspeicher fordert qualifizierte Zielgruppen aus der Zielgruppenbibliothek an (z. B. aus Adobe Analytics, Adobe Audience Manager freigegebene Zielgruppen usw.). |
| 7 | Das Akamai-CDN antwortet mit dem JSON-Regel-Artefakt. |
| 8 | Der Profilspeicher wird für die Zielgruppen-Qualifizierung und Bucketing zum Filtern von Aktivitäten verwendet. |
| 9 | Der resultierende Inhalt wird ausgewählt, nachdem das Erlebnis aus Live-[!DNL Target]-Aktivitäten ermittelt wurde. |
| 10 | Die at.js-Bibliothek blendet die entsprechenden Elemente auf der Seite aus, die mit dem Erlebnis verknüpft sind, das gerendert werden muss. |
| 11 | Die at.js-Bibliothek zeigt den Hauptteil an, sodass der Rest der Seite geladen werden kann, damit der Besucher ihn anzeigen kann. |
| 12 | Die at.js-Bibliothek bearbeitet das DOM, um das Erlebnis aus dem [!DNL Target]-Edge Network zu rendern. |
| 13 | Das Erlebnis wird für den Besucher dargestellt. |
| 14 | Die gesamte Webseite wird geladen. |
| 15 | Analytics-Daten werden an Datenerfassungs-Server gesendet. Zielgruppendaten werden über die SDID mit den Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet. Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

Das folgende Diagramm veranschaulicht die Interaktion zwischen Ihrem Besucher, dem Browser, at.js 2.5.0+ und dem zwischengespeicherten JSON-Regelartefakt für eine nachfolgende Seitennavigation oder einen erneuten Besuch. In diesem Diagramm sollten Sie sich nur auf den Anwendungsfall konzentrieren, dass eine geräteinterne Entscheidung für die nachfolgende Seitennavigation oder den erneuten Besuch getroffen wird. Beachten Sie, dass je nachdem, welche Aktivitäten für bestimmte Seiten aktiv sind, ein Server-seitiger Aufruf erfolgen kann, um Server-seitige Entscheidungen auszuführen.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Hybrides Flussdiagramm für nachfolgende Seitennavigation und Wiederholungsbesuche](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "Hybrides Flussdiagramm für nachfolgende Seitennavigation und Wiederholungsbesuche"){zoomable="yes"}

Die folgende Liste entspricht den Zahlen im Diagramm:

>[!NOTE]
>
>[!DNL Adobe Target] Admin-Server qualifizieren alle Ihre Aktivitäten, die für die [!UICONTROL on-device decisioning] infrage kommen, generieren das JSON-Regelartefakt und übertragen es an das Akamai-CDN. Ihre Aktivitäten werden kontinuierlich auf Aktualisierungen überwacht, um ein neues JSON-Regelartefakt auszugeben, das an das Akamai-CDN weitergegeben wird.

| Schritt | Beschreibung |
| --- | --- |
| 1 | Die Experience Cloud-Besucher-ID wird vom [Adobe Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) abgerufen. |
| 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen.<br />Die at.js-Bibliothek kann auch asynchron geladen werden, wobei ein optionales pre-hiding-Snippet auf der Seite implementiert ist. |
| 3 | Die at.js-Bibliothek blendet den Hauptteil aus, um Flackern zu verhindern. |
| 4 | Es wird eine Anfrage zum Abrufen eines Erlebnisses gestellt. |
| 5 | Die at.js-Bibliothek bestätigt, dass das JSON-Regelartefakt bereits zwischengespeichert wurde, und führt die Entscheidung im Speicher aus, um das Erlebnis abzurufen. |
| 6 | Die getesteten Elemente sind ausgeblendet. |
| 7 | Die at.js-Bibliothek zeigt den Hauptteil an, sodass der Rest der Seite geladen werden kann, damit der Besucher ihn anzeigen kann. |
| 8 | Die at.js-Bibliothek bearbeitet das DOM, um das Erlebnis aus dem zwischengespeicherten JSON-Regel-Artefakt zu rendern. |
| 9 | Das Erlebnis wird für den Besucher dargestellt. |
| 10 | Die gesamte Webseite wird geladen. |
| 11 | Analytics-Daten werden an Datenerfassungs-Server gesendet. Zielgruppendaten werden über die SDID mit den Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet. Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über [!UICONTROL Analytics for Target] (A4T)-Berichte angezeigt werden. |

## Wie aktiviere ich [!UICONTROL on-device decisioning]?

[!UICONTROL On-device decisioning] ist für alle [!DNL Target]-Kunden verfügbar, die at.js 2.5.0 oder höher verwenden.

So aktivieren Sie [!UICONTROL on-device decisioning]:

>[!NOTE]
>
>Sie müssen über die Admin- oder Genehmiger[Benutzerrolle verfügen, ](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) den Umschalter Geräteinterne Entscheidungsfindung zu aktivieren oder zu deaktivieren.

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Schieben Sie unter **[!UICONTROL Account details]** den Umschalter **[!UICONTROL On-Device Decisioning]** auf die Position „ein“.

   ![[!UICONTROL On-device decisioning] Umschalter](assets/on-device-decisioning-toggle.png)

   Die Option „Alle vorhandenen [!UICONTROL on-device decisioning] qualifizierten Aktivitäten in das Artefakt einbeziehen“ wird angezeigt, wenn Sie [!UICONTROL on-device decisioning] aktivieren.
1. (Bedingt) Schieben Sie den Umschalter auf die Position „Ein“, wenn alle Ihre Live [!DNL Target]-Aktivitäten, die für [!UICONTROL on-device decisioning] qualifiziert sind, automatisch in das Artefakt aufgenommen werden sollen.

   Wenn Sie diesen Umschalter deaktiviert lassen, müssen Sie alle [!UICONTROL on-device decisioning] Aktivitäten neu erstellen und aktivieren, damit sie in das generierte Regelartefakt aufgenommen werden. Mit anderen Worten: Aktivitäten, die sich vor dem Aktivieren des Umschalters Geräteinterne Entscheidungsfindung im Live-Status befinden, sind nicht im Regelartefakt enthalten.

Nach der Aktivierung des Umschalters „Geräteinterne Entscheidungsfindung“ beginnt [!DNL Target] mit der Generierung und Verbreitung [Regelartefakte](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) für Ihren Client.

>[!WARNING]
>
>Stellen Sie sicher, dass Sie den Umschalter aktivieren, bevor Sie die [!DNL Adobe Target] SDK für die Verwendung von [!UICONTROL on-device decisioning] initialisieren. Die Regelartefakte müssen zunächst generiert und an die Akamai-CDNs weitergegeben werden, [!UICONTROL on-device decisioning] sie funktionieren. Es kann fünf bis zehn Minuten dauern, bis das erste Regelartefakt generiert und an das Akamai-CDN weitergegeben wird.

## Wie konfiguriere ich at.js 2.5.0+ für [!UICONTROL on-device decisioning]?

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**.
1. Klicken Sie unter **[!UICONTROL Implementation Methods]** > **[!UICONTROL Main Implementation Method]** auf **[!UICONTROL Edit]** neben Ihrer at.js-Version (muss at.js 2.5.0 oder höher sein).

   ![Bearbeiten der Haupteinstellungen für Implementierungsmethoden](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >Bevor Sie diese Standardeinstellungen ändern, wenden Sie sich an die Kundenunterstützung, um zu vermeiden, dass Ihre aktuelle Implementierung beeinträchtigt wird.

1. Wählen Sie die gewünschte Entscheidungsmethode aus:

   * Nur Server-seitig
   * Nur auf dem Gerät
   * Hybrid

   ![Bedienfeld „at.js-Einstellungen bearbeiten“](assets/global-settings.png)

### Globale Einstellungen

Sie können eine standardmäßige Entscheidungsmethode für alle [!DNL Target] Entscheidungen konfigurieren. Die verschiedenen Entscheidungsmethoden sind nur Server-seitig, nur auf dem Gerät und Hybrid. Die in der [!DNL Target] Benutzeroberfläche ausgewählte Entscheidungsmethode wird in `window.targetGlobalSettings` unter dem Feld `decisioningMethod` konfiguriert. Weitere Informationen zum `decisioningMethod` finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### Benutzerdefinierte Einstellung

Wenn Sie die `decisioningMethod` in `window.targetGlobalSettings` festlegen, aber die `decisioningMethod` für jede [!DNL Adobe Target] Entscheidung entsprechend Ihrem Anwendungsfall überschreiben möchten, können Sie dieses Verfahren durchführen, indem Sie `decisioningMethod` im Aufruf [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) von at.js2.5.0+ angeben.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>Um „On-Device“ oder „Hybrid“ als Entscheidungsmethode im Aufruf von getOffers() zu verwenden, stellen Sie sicher, dass die globale Einstellung als „On-Device“ oder „Hybrid“ `decisioningMethod`. Die at.js-Bibliothek 2.5.0+ muss wissen, ob das JSON-Regelartefakt sofort nach dem Laden auf der Seite heruntergeladen und zwischengespeichert werden soll. Wenn die Entscheidungsmethode für die globale Einstellung auf „Server-seitig“ festgelegt ist und die Entscheidungsmethode „On-Device“ oder „Hybrid“ an den Aufruf „getOffers()“ übergeben wird, würde at.js 2.5.0+ nicht das JSON-Regel-Artefakt zwischengespeichert haben, um Ihre Entscheidungen auf dem Gerät auszuführen.

### Artefakt-Cache-TTL

Target stellt Ihre Aktivitäten dar, die für die [!UICONTROL on-device decisioning] als Artefakt qualifiziert sind, das aus Metadaten, Regeln und Bedingungen besteht. Dieses Artefakt wird im Akamai-CDN zwischengespeichert. Beim ersten Besuch Ihres Benutzers lädt der Browser des Benutzers das Artefakt, das Ihre [!UICONTROL on-device decisioning]-Aktivitäten darstellt, herunter und speichert es zwischen.

Bei nachfolgenden Besuchen Ihrer Site prüft der Browser automatisch, ob er eine neuere Version des Artefakts herunterladen muss. Diese Prüfung erhöht die Latenz. Die TTL für den Artefaktcache definiert die Anzahl der Minuten, die der Browser nicht auf ein aktualisiertes Artefakt seit dem letzten erfolgreichen Download überprüfen soll. Je länger der Zeitrahmen ist, desto besser ist die Leistung. Je kürzer der Zeitrahmen, desto besser die Datenfrische, aber auf Kosten der zusätzlichen Latenz.

## Woher weiß ich, dass eine Aktivität [!UICONTROL on-device decisioning] geeignet ist?

Nachdem Sie eine Aktivität erstellt haben, die [!UICONTROL on-device decisioning] geeignet ist, wird eine Beschriftung mit dem Titel On-Device Decisioning qualifiziert auf der Seite Überblick der Aktivität angezeigt.

![Kennzeichnung On-Device Decisioning auf der Seite Überblick der Aktivität.](assets/on-device-decisioning-eligible-label.png)

Dieser Titel bedeutet nicht, dass die Aktivität immer über [!UICONTROL on-device decisioning] zugestellt wird. Nur wenn at.js 2.5.0+ für die Verwendung von [!UICONTROL on-device decisioning] konfiguriert ist, wird diese Aktivität auf dem Gerät ausgeführt. Wenn at.js 2.5.0+ nicht für die Verwendung auf dem Gerät konfiguriert ist, wird diese Aktivität weiterhin über einen Server-Aufruf von at.js bereitgestellt.

Über den Filter On-Device Decisioning können Sie nach allen Aktivitäten filtern, die auf der Seite Aktivitäten [!UICONTROL on-device decisioning] geeignet sind.

![Auf der Seite „Aktivitäten“ kann ein Filter für On-Device Decisioning verwendet werden.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>Nachdem Sie eine Aktivität erstellt und aktiviert haben, die [!UICONTROL on-device decisioning] geeignet ist, kann es fünf bis zehn Minuten dauern, bis sie in das Regelartefakt aufgenommen wird, das generiert und an den Akamai-CDN-Punkt der Präsenzen übertragen wird.

## Zusammenfassung der Schritte zur Sicherstellung, dass meine [!UICONTROL on-device decisioning]-Aktivitäten über at.js 2.5.0 bereitgestellt werden+?

1. Rufen Sie die [!DNL Adobe Target]-Benutzeroberfläche auf und navigieren Sie zu **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account Details]** , um den Umschalter **[!UICONTROL On-Device Decisioning]** zu aktivieren.
1. Aktivieren Sie den Umschalter **[!UICONTROL "Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact"]** .

   Die erste Generierung eines JSON-Regelartefakts kann bis zu 10 Minuten dauern.

1. Erstellen und aktivieren Sie einen [Aktivitätstyp, der von [!UICONTROL on-device decisioning]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md) unterstützt wird, und stellen Sie sicher, dass er [!UICONTROL on-device decisioning] geeignet ist.
1. Legen Sie die **[!UICONTROL Decisioning Method]** über die Benutzeroberfläche „at.js-Einstellungen“ entweder auf **[!UICONTROL "Hybrid"]** oder **[!UICONTROL "On-device only"]** fest.
1. Laden Sie at.js 2.5.0+ herunter und stellen Sie es auf Ihren Seiten bereit.
