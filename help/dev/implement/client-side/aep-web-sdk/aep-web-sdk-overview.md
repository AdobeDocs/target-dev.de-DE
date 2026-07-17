---
keywords: Adobe Experience Platform Web SDK, AEP Web SDK, Web SDK, SDK, Adobe Experience Cloud, Platform Edge Network, Adobe Experience Platform Edge Network, Edge Network, AEP Edge Network, Adobe Experience Platform Web SDK0
description: Erfahren Sie, wie Sie mit der [!UICONTROL Adobe Experience Platform Web SDK] über die [!UICONTROL AEP Edge Network mit den verschiedenen Services [!UICONTROL Adobe Experience &#x200B;]) &#x200B;].
title: Wie implementiere ich mit dem [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
TQID: https://experienceleague.adobe.com/j3-KSuCkcyyTB2KG4Icm2E7xpAfcuPkaOlhxitd5q-4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: b6b447ccb88925a8efb6ff6a80ae475c8780dbc8
workflow-type: tm+mt
source-wordcount: 844
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von [!UICONTROL Adobe Experience Cloud] ermöglicht, über die [!UICONTROL Adobe Experience Platform Edge Network] mit den verschiedenen Services in der [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) zu interagieren. Zusätzlich zur JavaScript-Bibliothek steht eine Erweiterung [!UICONTROL Adobe Experience Platform] zur Verfügung, die Sie bei Ihren Web-SDK-Konfigurationen unterstützen kann.

>[!IMPORTANT]
>
>Bei der Implementierung von [!DNL Target] mit der [!UICONTROL Adobe Experience Platform Web SDK] durchlaufen Anfragen und Antworten die Interact-API (über den `sendEvent`-Befehl über die [!UICONTROL Experience Platform Edge Network]) und nicht [!DNL Target] [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md). Die [!DNL Delivery API] ist nur für [!DNL at.js] und direkte Server-seitige Implementierungen vorgesehen. Unter [Vergleichen der at.js-Bibliothek mit der Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) erfahren Sie, wie sich die beiden Ansätze unterscheiden.

Weitere Informationen finden Sie unter den folgenden Links in der Hilfe zu *[!UICONTROL Adobe Experience Platform Web SDK]*:

* Ausführliche Informationen: [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de)
* Spezifische Informationen für [!DNL Target]: [[!DNL Target] Übersicht](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=de)

## Tutorials

Die folgenden Tutorials helfen Ihnen bei der Implementierung:

### Implementieren von [!DNL Adobe Experience Cloud] mit [!DNL Platform Web SDK]

Erfahren Sie in diesem Tutorial, wie Sie [!DNL Experience Cloud]-Programme mithilfe von [!DNL Adobe Experience Platform Web SDK] [&#x200B; implementieren](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de). Spezifische Informationen zu [!DNL Target] finden Sie im Tutorial-Abschnitt [Einrichten [!DNL Target]  mit Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=de).

### Migrieren von [!DNL Target] aus at.js 2.*x* nach [!DNL Platform Web SDK]

Erfahren Sie in diesem Tutorial, wie Sie Ihre [!DNL Target]-Implementierung von at.js 2 *x* zum [!DNL Adobe Experience Platform Web SDK] [migrieren](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=de).

## Empfohlene Dokumentation

Zusätzlich zur oben erwähnten [!UICONTROL Platform Web SDK]-Dokumentation enthalten die Themen in diesem Handbuch auch spezifische Informationen zu [!UICONTROL Platform Web SDK] in Bezug auf [!DNL Target] Funktionen.

| Funktion | Beschreibung/Link |
| --- | --- |
| [Aktivitäts-QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=de) | Verwenden Sie QA-URLs in [!DNL Target], um eine einfache End-to-End-Aktivitäts-QA mit Vorschau-Links, die sich nie ändern, optionalem Audience-Targeting und QA-Berichten durchzuführen, die weiterhin aus Live-Aktivitätsdaten segmentiert sind. Aktivitäts-QA ermöglicht es Ihnen, Ihre [!DNL Target] Aktivitäten vollständig zu testen, bevor Sie sie live starten.<p>Siehe [Kompatibilität der Target JavaScript-Bibliothek mit dem QA-](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=de#compatibility) und [Vorschau-URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=de#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de) | [!UICONTROL Adobe Analytics for Target] (A4T) ist eine lösungsübergreifende Integration, mit der Sie Aktivitäten basierend auf [!DNL Analytics] Konversionsmetriken und Zielgruppensegmenten erstellen können. Mit der A4T-Integration können Sie Ihre Ergebnisse anhand von Analytics-Berichten überprüfen.<p>Siehe [Unterstützte Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de#section_F487896214BF4803AF78C552EF1669AA) und [Implementierungsschritte für eine Adobe Experience Platform Web SDK-Implementierung](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=de#platform). |
| [Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=de) | Zielgruppen in [!DNL Target] bestimmen, wer die Inhalte und Erlebnisse einer zielgerichteten Aktivität sieht.<p>Siehe [Verwenden der Liste „Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=de#use-list) und [Kombinieren mehrerer Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html?lang=de). |
| [Erstellen von Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=de) | Die Verwendung der in [!DNL Adobe Experience Platform] erstellten Zielgruppen liefert umfassendere Kundendaten, die zu einer wirkungsvolleren Personalisierung führen.<p>Siehe [Verwenden von Zielgruppen aus Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=de#aep). |
| [Angebotsentscheidungen](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=de) | Fügen Sie in [!DNL Adobe Journey Optimizer] erstellte Angebotsentscheidungen zu [!DNL Target] -Aktivitäten hinzu (manueller A/B-Test oder Erlebnis-Targeting), um das nächstbeste Angebot für Ihre Besucher im Web und auf Mobilgeräten zu ermitteln und bereitzustellen. |
| [Umleitungsangebote – Häufig gestellte Fragen zu A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html?lang=de) | Umleitungsangebote führen dazu, dass die Browser der Besucher zu einer neuen Seite umgeleitet werden.<p>Siehe [Unterstützt [!UICONTROL Adobe Experience Platform Web SDK] Umleitungsangebote für A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html?lang=de#platform) |
| [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de) | Mit Antwort-Token können Sie [!DNL Target] an Google Analytics und andere Drittanbieter-Integrationen senden.<p>Unter [Senden von Daten an Google Analytics über Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=de#sending-data-to-google-analytics-via-platform-web-sdk) finden Sie ein Codebeispiel für die Durchführung dieser Aufgabe. |
| [Implementierung von Einzelseitenanwendungen](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=de) im Handbuch *[!UICONTROL Platform Web &#x200B;]Übersicht* . | [!UICONTROL Adobe Experience Platform Web SDK] bietet umfangreiche Funktionen, mit denen Ihr Unternehmen Personalisierungen auf Client-seitigen Technologien der nächsten Generation wie Single Page Applications (SPAs) durchführen kann. |
| [Änderungen der TLS-Verschlüsselung (Transport Layer Security)](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | TLS (Transport Layer Security) hilft Ihnen, die höchsten Sicherheitsstandards aufrechtzuerhalten und die Sicherheit von Kundendaten zu fördern. |
