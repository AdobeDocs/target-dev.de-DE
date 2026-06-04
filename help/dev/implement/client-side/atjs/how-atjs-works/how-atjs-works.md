---
keywords: Systemdiagramm, Flimmern, at.js, Implementierung, JavaScript-Bibliothek, js, atjs, $8
description: Erfahren Sie, wie die  [!DNL Target] -JavaScript-Bibliothek (at.js), einschließlich Systemdiagrammen, funktioniert. Dies hilft Ihnen auch, den Workflow zum Laden von Seiten besser zu verstehen.
title: Wie funktioniert die JavaScript-Bibliothek at.js?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
TQID: https://experienceleague.adobe.com/ZyfwRiSeZDL-gFA-3MehXoNO5XhdANPaAmHqDxVeQ-g
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1220
ht-degree: 54%

---

# Funktionsweise von „at.js“

Zur Client-seitigen Implementierung von [!DNL Adobe Target] müssen Sie die JavaScript-Bibliothek „at.js“ verwenden.

Bei Client-seitigen Implementierungen von [!DNL Adobe Target] stellt [!DNL Target] die mit einer Aktivität verknüpften Erlebnisse direkt dem Client-Browser bereit. Der Browser entscheidet, welches Erlebnis angezeigt werden soll, und zeigt es an. Bei einer Client-seitigen Implementierung können Sie einen WYSIWYG-Editor, Visual [Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Ihre Tests und Personalisierungserlebnisse zu erstellen.

## Was ist at.js?

Die at.js-Bibliothek ist die Implementierungsbibliothek für die Client-seitige Implementierung von [!DNL Adobe Target]. Die at.js-Bibliothek sorgt für kürzere Seitenladezeiten bei Web-Implementierungen und bietet bessere Implementierungsoptionen für Single-Page-Anwendungen. „at.js“ ist die empfohlene Implementierungsbibliothek und wird häufig mit neuen Funktionen aktualisiert. Es wird empfohlen, dass alle -Kunden die [neueste Version von at.js) implementieren oder &#x200B;](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

Weitere Informationen finden Sie unter [JavaScript-Bibliotheken in Target](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#libraries).

In der [!DNL Target]unten dargestellten Implementierung sind die folgenden Adobe Experience Cloud-Lösungen implementiert: [!DNL Analytics], Target und [!DNL Audience Manager]. Darüber hinaus werden die folgenden [!DNL Experience Cloud] Core Services implementiert: [!DNL Adobe Experience Platform], [!UICONTROL Audiences] und [!UICONTROL Besucher-ID-].

## Was ist der Unterschied zwischen at.js 1.*x* und at.js 2.x-Workflow-Diagrammen?

Weitere [&#x200B; zu den Unterschieden, die in 2.O ab 1.x eingeführt wurden, finden Sie unter „Aktualisieren von at.js 1.x auf at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) **.

Grob betrachtet gibt es einige Unterschiede zwischen den beiden Versionen:

* at.js 2.x hat kein globales Mbox-Anfragekonzept, sondern stellt Anfragen beim Laden der Seite. Eine Anfrage beim Laden der Seite kann als Anfrage zum Abrufen von Inhalten verstanden werden, die beim ersten Laden Ihrer Website angewendet werden soll.
* at.js 2.x verwaltet Konzepte mit dem Namen [!UICONTROL Ansichten], die für Single Page Applications (SPAs) verwendet werden. at.js 1.*x* ist dieses Konzept nicht bekannt.

## Diagramme in at.js 2.x

Die folgenden Diagramme helfen Ihnen, den Workflow von at.js 2.x mit [!UICONTROL Ansichten] zu verstehen und zu verstehen, wie dies die SPA-Integration verbessert. Eine bessere Einführung in die in at.js 2.x verwendeten Konzepte finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Target-Fluss mit at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "Target-Fluss mit at.js 2.x"){zoomable="yes"}

| Schritt | Details |
| --- | --- |
| 1 | Ein Aufruf gibt die [!UICONTROL Experience Cloud-ID] zurück, wenn der Benutzer authentifiziert ist. Ein anderer Aufruf synchronisiert die Kunden-ID. |
| 2 | Die at.js-Bibliothek wird synchron geladen und blendet den Dokumentkörper aus.<br />at.js kann auch asynchron geladen werden, wobei ein optionales Code-Ausschnitt zum Vorab-Ausblenden auf der Seite implementiert wird. |
| 3 | Es wird eine Seitenlade-Anfrage durchgeführt, in der alle konfigurierten Parameter (MCID, SDID und Kunden-ID) enthalten sind. |
| 4 | Profilskripte werden ausgeführt und gehen dann in den [!UICONTROL Profilspeicher]. Der Storere fordert qualifizierte Zielgruppen aus der [!UICONTROL Zielgruppenbibliothek] an (z. B. aus [!DNL Adobe Analytics], [!DNL Audience Manager] usw. freigegebene Zielgruppen).<br />Kundenattribute werden in einem Batch-Prozess an den [!UICONTROL Profilspeicher] gesendet. |
| 5 | Basierend auf den URL-Anfrageparametern und den Profildaten entscheidet [!DNL Target], welche Aktivitäten und Erlebnisse für die aktuelle Seite und zukünftige Ansichten an den Besucher zurückgegeben werden sollen. |
| 6 | Zielgerichteter Inhalt wird zurück an die Seite übermittelt. Dieser enthält optional Profilwerte für eine weitere Personalisierung.<br />Die zielgerichteten Inhalte auf der aktuellen Seite werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern.<br />Zielgerichtete Inhalte für Ansichten, die als Ergebnis von Benutzeraktionen in einer SPA angezeigt werden, werden im Browser zwischengespeichert, sodass die SPA sofort ohne zusätzlichen Server-Aufruf angezeigt werden kann, wenn die Ansichten durch `triggerView()` ausgelöst werden. |
| 7 | Analytics-Daten werden an Server [!UICONTROL Datenerfassung] gesendet. |
| 8 | Zielgruppendaten werden über die SDID mit Analytics-Daten abgeglichen und in den [!DNL Analytics]-Reporting-Speicher verarbeitet.<br />[!DNL Analytics] -Daten können dann sowohl in [!DNL Analytics] als auch in [!DNL Target] über (A4T)-Berichte angezeigt werden. |

Jetzt werden, wo immer `triggerView()` in Ihrer SPA implementiert ist, die [!UICONTROL Ansichten] und Aktionen aus dem Cache abgerufen und dem Benutzer ohne Server-Aufruf angezeigt. `triggerView()` sendet außerdem eine Benachrichtigungsanfrage an das [!DNL Target]-Back-End, um Impressions-Zählungen zu erhöhen und aufzuzeichnen. Weitere Informationen zu at.js für SPAs mit Ansichten finden Sie unter [Implementieren von Einzelseiten-Apps](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Target flow at.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target flow at.js 2.x triggerView"){zoomable="yes"}

| Schritt | Details |
| --- | --- |
| 1 | `triggerView()` wird in der SPA aufgerufen, um die [!UICONTROL Ansicht“ zu rendern &#x200B;] Aktionen anzuwenden, um visuelle Elemente zu ändern. |
| 2 | Gezielte Inhalte für die Ansicht werden aus dem Cache gelesen. |
| 3 | Die zielgerichteten Inhalte werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern. |
| 4 | Eine Benachrichtigungsanfrage wird an den [!DNL Target]Profilspeicher[!UICONTROL &#x200B; gesendet, &#x200B;] den Besucher in der Aktivitäts- und Inkrementmetrik zu zählen. |
| 5 | [!DNL Analytics] Daten an [!UICONTROL Datenerfassungs-Server] gesendet. |
| 6 | [!DNL Target] Daten werden über die SDID mit [!DNL Analytics] Daten abgeglichen und in den [!DNL Analytics]-Reporting-Speicher verarbeitet. [!DNL Analytics] Daten können dann sowohl in [!DNL Analytics] als auch [!DNL Target] über A4T-Berichte angezeigt werden. |

### Video: Architekturdiagramm von at.js 2.x

at.js 2.x verbessert die Unterstützung von Adobe Target für SPAs und kann mit anderen Experience Cloud-Lösungen integriert werden. In diesem Video wird erklärt, wie alles zusammenkommt.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

Weitere Informationen finden Sie unter [Funktionsweise von at.js 2.x](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html).

## at.js 1.x-Diagramm

Die folgenden Diagramme helfen Ihnen, den Workflow von at.js 1.x besser zu verstehen.

(Klicken Sie auf das Bild, um es auf die volle Breite zu erweitern.)

![Target-Fluss at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Target-Fluss at.js 1.x"){zoomable="yes"}

| Schritt | Beschreibung | Aufruf | Beschreibung |
|--- |--- |--- |--- |
| 1 | Ein Aufruf gibt die Experience Cloud-ID (MCID) zurück, wenn der Benutzer authentifiziert ist. Ein weiterer Aufruf synchronisiert die Kunden-ID. | 2 | Die Bibliothek at.js wird synchron geladen und im Dokumentenkörper verborgen. |
| 3 | Es wird ein globaler Mbox-Aufruf durchgeführt, in dem alle konfigurierten Parameter, MCID, SDID und Kunden-IDs enthalten sind (optional). | 4 | Profilskripte werden ausgeführt und anschließend in den Profilspeicher eingespeist. Der Store fordert qualifizierte Zielgruppen aus der Zielgruppenbibliothek an (z. B. von Adobe Analytics, Audience Manager freigegebene Zielgruppen usw.). <br />Kundenattribute werden in einem Batch-Prozess an den Profilspeicher gesendet. |
| 5 | Basierend auf URL, Mbox-Parametern und Profildaten wird von [!DNL Target] entschieden, welche Aktivitäten und Erlebnisse dem Besucher angezeigt werden sollen. | 6 | Zielgerichteter Inhalt wird zurück an die Seite übermittelt. Dieser enthält optional Profilwerte für eine weitere Personalisierung.<br />Das Erlebnis wird so schnell wie möglich ohne ein Flackern der Standardinhalte bereitgestellt. |
| 7 | Analytics-Daten werden an Datenerfassungsserver übermittelt. | 8 | Zieldaten werden über die SDID mit Analytics-Daten abgeglichen und in den Analytics-Reporting-Speicher verarbeitet.<br />Analytics-Daten können dann sowohl in Analytics als auch in [!DNL Target] über Berichte [!UICONTROL Analytics for Target] (A4T) angezeigt werden. |

### Video – Office Hours: Tipps und Übersicht zu at.js (26. Juni 2019)

Dieses Video ist eine Aufzeichnung von „Office Hours“, einer Initiative, die vom Team der [!UICONTROL Adobe-] geleitet wird.

* Vorteile der Verwendung von at.js
* at.js-Einstellungen
* Einstellungen bei Flackern
* Debuggen von „at.js“
* Bekannte Probleme
* FAQs

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## Darstellung von Angeboten mit HTML-Inhalten durch at.js

Bei der Darstellung von Angeboten mit HTML-Inhalten wendet at.js den folgenden Algorithmus an:

1. Bilder werden vorab geladen (wenn `<img>`-Tags in HTML-Inhalten vorhanden sind).

1. HTML-Inhalte sind mit dem DOM-Knoten verbunden.

1. Inline-Skripte werden ausgeführt (Code, der in `<script>`-Tags eingeschlossen ist).

1. Remote-Skripte werden asynchron geladen und ausgeführt (`<script>`-Tags mit `src`-Attributen).

Wichtige Hinweise:

* at.js garantiert nicht die Reihenfolge der Ausführung von Remote-Skripten, da diese asynchron geladen werden.
* Inline-Skripte sollten nicht von Remote-Skripten abhängig sein, da diese später geladen und ausgeführt werden.
