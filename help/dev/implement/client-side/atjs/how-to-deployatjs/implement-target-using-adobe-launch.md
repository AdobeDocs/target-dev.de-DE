---
keywords: Implementieren, Implementierung, Adobe Launch, Launch, Race, Redirect, Experience Platform Launch, Platform Launch, Tags, Adobe Platform, Implementierung2
description: Erfahren Sie, wie Sie die at [!DNL Adobe Target] js-Bibliothek mithilfe von  [!DNL Adobe Experience Platform], der bevorzugten Methode zur Implementierung von Target, implementieren.
title: Wie implementiere ich  [!DNL Target]  mit  [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
TQID: https://experienceleague.adobe.com/5dXJlXYYvlu5sskrNED2j55SNmeggtWTb1jLgXRXAEo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 61%

---

# Implementieren von [!DNL Target] mithilfe von [!DNL Adobe Experience Platform]

Tags in [!DNL Adobe Experience Platform] sind die nächste Generation von Tag-Management-Funktionen von [!DNL Adobe]. Launch bietet Kunden eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die zur Unterstützung entsprechender Kundenerlebnisse erforderlich sind.

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als Suite von Datenerfassungstechnologien in [!DNL Adobe Experience Platform] umbenannt. Dies spiegelt sich in der Produktdokumentation in verschiedenen Änderungen hinsichtlich der verwendeten Begriffe wider. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?).

In der folgenden Tabelle finden Sie verschiedene Quellen, über die Sie weitere Informationen abrufen können:

| Ressource | Details |
|--- |--- |
| [Adobe Target hinzufügen](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html?lang=de#implement-solutions) | Diese Anleitung enthält schrittweise Anweisungen zur Implementierung von [!DNL Target] auf einer Website mit Tags in [!DNL Adobe Experience Platform]. Die Themen umfassen unter anderem das Hinzufügen der at.js-JavaScript-Bibliothek, das Auslösen der globalen Mbox, das Hinzufügen von Parametern und die Integration mit anderen Lösungen. Dieser Artikel ist Teil eines größeren Tutorials, in dem Sie erfahren, wie Sie Adobe Experience Platform und andere Adobe Experience Cloud-Lösungen implementieren. |
| [Schnellstartanleitung](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html?lang=de) | Informationen zur Bereitstellung und Verwaltung der Analyse-, Marketing- und Werbe-Tags, die zur Unterstützung relevanter Kundenerlebnisse erforderlich sind. |
| [Adobe  [!DNL Target] -Erweiterungen – Überblick](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=de) | Informationen zur Implementierung von [!DNL Target] mit [!DNL Adobe Experience Platform]. |

## Vorteile der Implementierung von at.js mit der [!DNL Target]-Erweiterung

Folgende Vorteile erzielen Sie nur, wenn Sie Tags in [!DNL Adobe Experience Platform] für die Implementierung von at.js verwenden. Aus diesem Grund empfiehlt Adobe dringend, Tags in [!DNL Adobe Experience Platform] anstelle einer manuellen Implementierung von at.js zu verwenden.

* **Behebt [!DNL Adobe Analytics] und Wettbewerbssituationen [!DNL Target]:** Da der [!DNL Analytics]-Aufruf vor dem [!DNL Target]-Aufruf ausgelöst werden kann, ist der [!DNL Target]-Aufruf nicht an den [!DNL Analytics]-Aufruf gebunden. Dies kann zu falschen Daten führen. Die Erweiterung [!DNL Target] stellt sicher, dass der Beacon-Aufruf [!DNL Analytics] wartet, bis der Aufruf [!DNL Target] abgeschlossen wurde (egal ob erfolgreich oder nicht). Die Verwendung von Tags in [!DNL Adobe Experience Platform] ist eine Lösung bezüglich der Dateninkonsistenz, die Kunden bei der manuellen Implementierung erleben können.

  >[!NOTE]
  >
  >Verwenden Sie die Aktion Beacon senden in der [!DNL Adobe Analytics]-Erweiterung, damit der [!DNL Analytics]-Aufruf auf den [!DNL Target]-Aufruf wartet. Wenn Sie `s.t()` oder `s.tl()` direkt mit benutzerdefiniertem Code aufrufen, warten [!DNL Analytics]-Aufrufe nicht, bis [!DNL Target]-Aufrufe abgeschlossen sind.

* **Verhindert fehlerhafte Verarbeitung von Umleitungsangeboten:** Wenn Sie [!DNL Target] und [!DNL Analytics] auf einer Seite haben und ein Umleitungsangebot von Target ausgeführt wird, kann eine Situation entstehen, in der der [!DNL Analytics]-Tracker fälschlicherweise eine Anfrage auslöst (da der Benutzer an eine andere URL umgeleitet wird). Wenn Sie [!DNL Target] und [!DNL Analytics] über Tags in [!DNL Adobe Experience Platform] implementieren, tritt dieses Problem nicht auf. Mithilfe von Tags in [!DNL Adobe Experience Platform] weist [!DNL Target] [!DNL Analytics] an, die [!DNL Analytics]-Beacon-Anforderung abzubrechen.


