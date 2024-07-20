---
keywords: Adobe Experience Platform Web SDK, aep Web SDK, Web SDK, SDK, Adobe Experience Cloud, Platform Edge Network, Adobe Experience Platform Edge Network, Edge Network, Aep Edge Network, Adobe Experience Platform Web SDK0
description: Erfahren Sie, wie Sie die [!UICONTROL Adobe Experience Platform Web SDK] verwenden, um mit den verschiedenen Diensten in der [!UICONTROL Adobe Experience Cloud] durch die [!UICONTROL AEP Edge Network] zu interagieren.
title: Wie implementiere ich den [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von [!UICONTROL Adobe Experience Cloud] ermöglicht, mit den verschiedenen Diensten in der [!DNL Adobe Experience Cloud] (einschließlich [!DNL Target]) über die [!UICONTROL Adobe Experience Platform Edge Network] zu interagieren. Zusätzlich zur JavaScript-Bibliothek gibt es eine [!UICONTROL Adobe Experience Platform] -Erweiterung, die Sie bei Ihren Web SDK-Konfigurationen unterstützen kann.

Weitere Informationen finden Sie unter den folgenden Links in der Hilfe zu *[!UICONTROL Adobe Experience Platform Web SDK]*:

* Umfassende Informationen: [Was ist [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de)
* Spezifische Informationen zu [!DNL Target]: [[!DNL Target] Übersicht](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=de)

## Tutorials

Die folgenden Tutorials helfen Ihnen bei der Implementierung:

### Implementieren von [!DNL Adobe Experience Cloud] mit [!DNL Platform Web SDK]

Erfahren Sie, wie Sie [!DNL Experience Cloud]-Anwendungen mit [!DNL Adobe Experience Platform Web SDK] in [diesem Tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) implementieren. Spezifische Informationen zu [!DNL Target] finden Sie im Tutorial-Abschnitt mit dem Titel [Einrichten [!DNL Target]  mit dem Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) .

### Migration von [!DNL Target] von at.js 2.*x* bis [!DNL Platform Web SDK]

Erfahren Sie, wie Sie Ihre [!DNL Target] -Implementierung von at.js 2 migrieren.*x* auf die [!DNL Adobe Experience Platform Web SDK] mit [diesem Tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=de).

## Empfohlene Dokumentation

Neben der oben erwähnten [!UICONTROL Platform Web SDK] -Dokumentation enthalten Themen in diesem Handbuch auch Informationen, die spezifisch für die [!UICONTROL Platform Web SDK] sind, da sie sich auf [!DNL Target] -Funktionen beziehen.

| Funktion | Beschreibung/Link |
| --- | --- |
| [Aktivitäts-QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | Verwenden Sie QA-URLs in [!DNL Target], um einfache End-to-End-Aktivitäts-QAs mit unveränderbaren Vorschaulinks, optionalem Zielgruppen-Targeting und QA-Berichten durchzuführen, die basierend auf Live-Aktivitätsdaten segmentiert bleiben. Mit Aktivitäts-QA können Sie Ihre [!DNL Target] -Aktivitäten vollständig testen, bevor Sie sie live schalten.<p>Siehe [Kompatibilität des JavaScript-Bibliotheks-QA-Modus für Target ](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) und [Vorschau-URLs anzeigen](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) ist eine lösungsübergreifende Integration, die Ihnen das Erstellen von Aktivitäten ermöglicht, die auf Konversionsmetriken und Zielgruppensegmenten aus [!DNL Analytics] basieren. Mit der A4T-Integration können Sie Analytics-Berichte verwenden, um Ihre Ergebnisse zu untersuchen.<p>Siehe [Unterstützte Aktivitätstypen](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) und [Implementierungsschritte für eine Adobe Experience Platform Web SDK-Implementierung](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | Zielgruppen in [!DNL Target] bestimmen, wer Inhalte und Erlebnisse in einer zielgerichteten Aktivität sieht.<p>Siehe [Verwenden der Zielgruppenliste](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) und [Kombinieren mehrerer Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [Erstellen von Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=de) | Die Verwendung von in [!DNL Adobe Experience Platform] erstellten Zielgruppen bietet umfassendere Kundendaten, die zu einer wirkungsvolleren Personalisierung führen.<p>Siehe [Verwenden von Zielgruppen aus Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [Angebotsentscheidungen](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | Fügen Sie in [!DNL Adobe Journey Optimizer] erstellte Angebotsentscheidungen zu [!DNL Target] -Aktivitäten hinzu (manueller A/B-Test oder Erlebnis-Targeting), um das nächste beste Angebot für Ihre Besucher im Web und auf Mobilgeräten zu ermitteln und bereitzustellen. |
| [Umleitungsangebote – Häufig gestellte Fragen zu A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | Umleitungsangebote führen dazu, dass die Browser der Besucher zu einer neuen Seite umleiten.<p>Siehe [Unterstützt [!UICONTROL Adobe Experience Platform Web SDK] Umleitungsangebote für A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [Antwort-Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | Mit Antwort-Token können Sie [!DNL Target] -Daten an Google Analytics und andere Drittanbieter-Integrationen senden.<p>Unter [Senden von Daten an Google Analytics über Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) finden Sie ein Codebeispiel für die Ausführung dieser Aufgabe. |
| [Implementierung einer Einzelseitenanwendung](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) im Leitfaden *[!UICONTROL Platform Web SDK]Übersicht* . | [!UICONTROL Adobe Experience Platform Web SDK] bietet umfassende Funktionen, mit denen Ihr Unternehmen Personalisierungen auf clientseitigen Technologien der nächsten Generation ausführen kann, wie z. B. Einzelseitenanwendungen (SPA). |
| [Änderungen der TLS-Verschlüsselung (Transport Layer Security)](../../before-implement/tls-transport-layer-security-encryption.md) | Mit TLS (Transport Layer Security) können Sie die höchsten Sicherheitsstandards einhalten und die Sicherheit von Kundendaten fördern. |
