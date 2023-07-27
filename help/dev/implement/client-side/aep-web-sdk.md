---
keywords: Adobe Experience Platform Web SDK, aep Web SDK, Web SDK, SDK, Adobe Experience Cloud, Platform Edge Network, Adobe Experience Platform Edge Network, Edge Network, Aep Edge Network, Adobe Experience Platform Web SDK0
description: Erfahren Sie, wie Sie die [!UICONTROL Adobe Experience Platform Web SDK] zur Interaktion mit den verschiedenen Diensten im [!UICONTROL Adobe Experience Cloud] durch die [!UICONTROL AEP Edge Network].
title: Implementieren mit der [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 12%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) ist eine clientseitige JavaScript-Bibliothek, die Kunden von [!UICONTROL Adobe Experience Cloud] zur Interaktion mit den verschiedenen Diensten im [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) durch die [!UICONTROL Adobe Experience Platform Edge Network]. Zusätzlich zur JavaScript-Bibliothek gibt es eine [!UICONTROL Adobe Experience Platform] -Erweiterung, um Sie bei Ihren Web SDK-Konfigurationen zu unterstützen.

Weitere Informationen finden Sie unter den folgenden Links in der *[!UICONTROL Adobe Experience Platform Web SDK]* help:

* Umfassende Informationen: [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de)
* Für spezifische Informationen [!DNL Target]: [[!DNL Target] Übersicht](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=de)

## Tutorials

Die folgenden Tutorials helfen Ihnen bei der Implementierung:

### Implementierung [!DNL Adobe Experience Cloud] mit [!DNL Platform Web SDK]

Erfahren Sie, wie Sie [!DNL Experience Cloud] Anwendungen, die [!DNL Adobe Experience Platform Web SDK] mit [dieses Tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Für spezifische Informationen [!DNL Target]finden Sie im Abschnitt des Tutorials mit dem Titel [Einrichten [!DNL Target] mit Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrieren [!DNL Target] von at.js 2.*x* nach [!DNL Platform Web SDK]

Erfahren Sie, wie Sie Ihre [!DNL Target] Implementierung von at.js 2.*x* der [!DNL Adobe Experience Platform Web SDK] mit [dieses Tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=de).

## Empfohlene Dokumentation

Zusätzlich zu den [!UICONTROL Platform Web SDK] Die oben genannten Dokumentationen enthalten auch Themen in diesem Handbuch Informationen zu [!UICONTROL Platform Web SDK] in Bezug auf [!DNL Target] Funktionen.

| Funktion | Beschreibung/Link |
| --- | --- |
| [Aktivitäts-QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Verwenden von QA-URLs in [!DNL Target] zur einfachen End-to-End-Aktivitäts-QA mit unveränderbaren Vorschaulinks, optionalem Zielgruppen-Targeting und QA-Berichten, die basierend auf Live-Aktivitätsdaten segmentiert bleiben. Mit Aktivitäts-QA können Sie Ihre [!DNL Target] -Aktivitäten, bevor sie live geschaltet werden.<p>Siehe [Kompatibilität des JavaScript-Bibliotheks-QA-Modus in Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) und [Vorschau-URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [Analytics for Target (A4T) ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics für Target] (A4T) ist eine lösungsübergreifende Integration, mit der Sie Aktivitäten basierend auf [!DNL Analytics] Konversionsmetriken und Zielgruppensegmente. Mit der A4T-Integration können Sie Ihre Ergebnisse anhand von Analytics-Berichten überprüfen.<p>Siehe [Unterstützte Aktivitättypen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) und [Implementierungsschritte für eine Adobe Experience Platform Web SDK-Implementierung](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Zielgruppen in [!DNL Target] bestimmen, wer Inhalte und Erlebnisse in einer zielgerichteten Aktivität sieht.<p>Siehe [Verwenden der Zielgruppenliste](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) und [Kombinieren mehrerer Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Erstellen von Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=de) | Die Verwendung der in [!DNL Adobe Experience Platform] erstellten Audiences liefert umfassendere Kundendaten, die zu einer wirkungsvolleren Personalisierung führen.<p>Siehe [Verwenden von Zielgruppen aus Adobe Experience Platform](https://experienceleague.adobe.com/docs/?lang=detarget/using/audiences/create-audiences/audiences.html#aep). |
| [Angebotsentscheidungen](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Hinzufügen von Angebotsentscheidungen, die in erstellt wurden [!DNL Adobe Journey Optimizer] nach [!DNL Target] Aktivitäten (manueller A/B-Test oder Erlebnis-Targeting) verwenden, um das nächste beste Angebot für Ihre Besucher im Web und auf Mobilgeräten zu ermitteln und bereitzustellen. |
| [Umleitungsangebote – Häufig gestellte Fragen zu A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Umleitungsangebote führen dazu, dass die Browser der Besucher zu einer neuen Seite umleiten.<p>Siehe [Führt die [!UICONTROL Adobe Experience Platform Web SDK] Unterstützung von Umleitungsangeboten für A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Antwort-Token ermöglichen den Versand von [!DNL Target] Daten an Google Analytics und andere Drittanbieterintegrationen weitergeben.<p>Siehe [Senden von Daten an Google Analytics über das Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) um ein Codebeispiel für die Ausführung dieser Aufgabe anzuzeigen. |
| [Implementierung von Einzelseiten-Apps](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) im *[!UICONTROL Platform Web SDK] Übersicht* Handbuch. | [!UICONTROL Adobe Experience Platform Web SDK] bietet umfassende Funktionen, mit denen Ihr Unternehmen mithilfe von Client-seitigen Technologien der nächsten Generation Personalisierungen ausführen kann, wie z. B. Einzelseitenanwendungen (SPA). |
| [Änderungen der TLS-Verschlüsselung (Transport Layer Security)](../../before-implement/tls-transport-layer-security-encryption.md) | Mit TLS (Transport Layer Security) können Sie die höchsten Sicherheitsstandards einhalten und die Sicherheit von Kundendaten fördern. |
