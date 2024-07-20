---
keywords: „at.js“-Integration, unterstützte Integrationen, nicht unterstützte Integrationen, Drittanbieterintegrationen
description: Weitere Informationen finden Sie unter den von  [!DNL Adobe Target] at.js unterstützten (und nicht unterstützten) Integrationen, darunter [!UICONTROL Analytics for Target] (A4T), [!UICONTROL Experience Cloud ID Service] und mehr.
title: Welche Integrationen unterstützt at.js?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 52%

---

# „at.js“-Integrationen

In diesem Artikel werden gängige Integrationen mit [!DNL Adobe Target] und der jeweilige Status der Unterstützung mit at.js beschrieben.

Wenn Sie eine Integration benötigen, die nicht unterstützt oder hier nicht erwähnt wird, wenden Sie sich an Ihren Kundenbetreuer oder Berater.

## Unterstützte Integrationen

| Integration | Details |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Siehe [Adobe Analytics als Berichtsquelle für Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). |
| [!UICONTROL Profiles & Audiences] (P&amp;A) | Siehe [Zielgruppen](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=de) im *Benutzerhandbuch für zentrale Dienste*. |
| [!UICONTROL Experience Cloud ID Service] | Siehe [Dokumentation des Adobe Experience Cloud ID-Service](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| [!UICONTROL Tags in Adobe Experience Platform] | [!UICONTROL Tags in Adobe Experience Platform] sind die nächste Generation der Tag-Management-Funktionen von [!DNL Adobe]. [!UICONTROL Tags] bietet Kunden eine einfache Möglichkeit, die Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die zur Unterstützung entsprechender Kundenerlebnisse erforderlich sind. Siehe [Implementieren [!DNL Target] mit Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | Die [!UICONTROL AEM Cloud Service] ermöglicht die Erstellung von [!UICONTROL A/B Test] - und [!UICONTROL Experience Targeting] -Aktivitäten innerhalb des AEM-Workflows. Unterstützt at.js mit [!UICONTROL Adobe Experience Manager] 6.2 mit FP-11577 (oder höher). Weitere Informationen finden Sie unter [Integrieren mit  [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=de) und wählen Sie Ihre AEM aus. |
| [!UICONTROL AEM Experience Fragments] | Mit in AEM in [!DNL Target] -Aktivitäten erstellten Experience Fragments können Sie die Benutzerfreundlichkeit und Leistungsfähigkeit von AEM mit den leistungsstarken Funktionen der automatisierten Intelligenz (AI) und des maschinellen Lernens (ML) in [!DNL Target] kombinieren, um Erlebnisse bedarfsgerecht zu testen und zu personalisieren.  AEM kombiniert all Ihre Inhalte und Assets an einer zentralen Stelle, um Ihre Personalisierungsstrategie zu begünstigen. Mit AEM können Sie an einer Stelle problemlos Inhalte für Desktops, Tablets und mobile Geräte erstellen, ohne Code zu schreiben. Es ist nicht erforderlich, Seiten für jedes Gerät zu erstellen. AEM passt jedes Erlebnis automatisch an Ihren Inhalt an.  Weitere Informationen finden Sie unter [AEM-Erlebnisfragmente](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html). |

## Nicht unterstützte Integrationen

| Integration | Details |
|--- |--- |
| Alte Integration von [!DNL Target] in [!DNL SiteCatalyst] | Hierbei handelte es sich um die Integration, bei der Kampagnen- und Rezept-IDs über den Seitenaufruf an [!DNL SiteCatalyst] gesendet wurden, damit Berichte über die Benutzeroberfläche von [!DNL SiteCatalyst] erstellt werden konnten. Diese Funktionalität wird durch A4T ersetzt. |
| Alte Integration von [!DNL Target] in [!DNL SiteCatalyst] | Hierbei handelte es sich um die Integration, die Mbox-Aufrufe namens `"SiteCatalyst: Event"` und `"SiteCatalyst: Purchase"` tätigte, damit Sie Erfolgsmetriken und Benutzerprofile auf Grundlage von eVars und Eigenschaften erstellen konnten. Diese Funktionalität wird durch A4T und P&amp;A ersetzt. |
| Alte Integration von [!DNL Audience Manager] (AAM) mit [!DNL Target] | Hierbei handelte es sich um die Integration, die Frontend-API-Aufrufe tätigte, um AAM-Segmente abzurufen, und diese anschließend als Mbox-Parameter bei jedem Mbox-Aufruf an die Seite sendete. |

## Drittanbieterintegrationen

| Integration | Details |
|--- |--- |
| Andere Tag-Manager | „at.js“ sollte auch mit anderen Tag-Management-plattformen funktionieren, die nicht von Adobe stammen, grundsätzlich sollten Sie beim Einsatz benutzerdefinierter Integrationsfunktionen, die von anderen Anbietern entwickelt wurden, jedoch vorsichtig sein. Deren Integrationen sind möglicherweise von internen mbox.js-Funktionen abhängig, die es in at.js nicht mehr gibt. |
| Drittanbieter für Daten (z. B. Demandbase, BlueKai, Wetter-APIs) | Viele Drittanbieter für Daten, die zur Ergänzung der Target-Benutzerprofile verwendet werden, können mithilfe der Funktion at.js [Datenanbieter](../atjs-functions/targetglobalsettings.md#data-providers) integriert werden. |
