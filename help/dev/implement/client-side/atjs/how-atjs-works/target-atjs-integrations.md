---
keywords: „at.js“-Integration, unterstützte Integrationen, nicht unterstützte Integrationen, Drittanbieterintegrationen
description: Hier finden Sie Informationen zu den von at. [!DNL Adobe Target]  unterstützten (und nicht unterstützten) Integrationen, einschließlich [!UICONTROL Analytics for Target] (A4T), der [!UICONTROL Experience Cloud ID Service] und mehr.
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
| [!UICONTROL Analytics for Target] (A4T) | Siehe [Adobe Analytics als Berichtsquelle für Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de). |
| [!UICONTROL Profiles & Audiences] (P&amp;A) | Siehe [Zielgruppen](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=de) im *Core Services-Benutzerhandbuch*. |
| [!UICONTROL Experience Cloud ID Service] | Siehe [Dokumentation des Adobe Experience Cloud ID-Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=de). |
| [!UICONTROL Tags in Adobe Experience Platform] | [!UICONTROL Tags in Adobe Experience Platform] sind die nächste Generation von Tag-Management-Funktionen von [!DNL Adobe]. [!UICONTROL Tags] bieten Kunden eine einfache Möglichkeit, die Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind. Siehe [Implementieren  [!DNL Target]  Verwenden von Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | Die [!UICONTROL AEM Cloud Service] ermöglicht die Erstellung von [!UICONTROL A/B Test]- und [!UICONTROL Experience Targeting] im AEM-Workflow. Unterstützt at.js mit [!UICONTROL Adobe Experience Manager] 6.2 mit FP-11577 (oder höher). Weitere Informationen finden Sie unter &quot;[ mit“  [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=de) wählen Sie Ihre AEM-Version aus. |
| [!UICONTROL AEM Experience Fragments] | Experience Fragments, die in AEM in [!DNL Target]-Aktivitäten erstellt wurden, ermöglichen es Ihnen, die Benutzerfreundlichkeit und Leistungsfähigkeit von AEM mit den leistungsstarken Funktionen für Automated Intelligence (KI) und maschinelles Lernen (ML) zu kombinieren, [!DNL Target] Erlebnisse in großem Umfang zu testen und zu personalisieren.  AEM kombiniert all Ihre Inhalte und Assets an einer zentralen Stelle, um Ihre Personalisierungsstrategie zu begünstigen. Mit AEM können Sie an einer Stelle problemlos Inhalte für Desktops, Tablets und mobile Geräte erstellen, ohne Code zu schreiben. Es ist nicht erforderlich, Seiten für jedes Gerät zu erstellen - AEM passt jedes Erlebnis automatisch an Ihre Inhalte an.  Weitere Informationen finden Sie unter [AEM-Erlebnisfragmente](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=de). |

## Nicht unterstützte Integrationen

| Integration | Details |
|--- |--- |
| Legacy-[!DNL Target] für [!DNL SiteCatalyst] Integration | Dies war die Integration, die Kampagnen- und Rezept-IDs über den Seitenaufruf an [!DNL SiteCatalyst] gesendet hat, damit Sie Berichte in der [!DNL SiteCatalyst]-Benutzeroberfläche erstellen können. Diese Funktionalität wird durch A4T ersetzt. |
| Legacy-[!DNL Target] für [!DNL SiteCatalyst] Integration | Hierbei handelte es sich um die Integration, die Mbox-Aufrufe namens `"SiteCatalyst: Event"` und `"SiteCatalyst: Purchase"` tätigte, damit Sie Erfolgsmetriken und Benutzerprofile auf Grundlage von eVars und Eigenschaften erstellen konnten. Diese Funktionalität wird durch A4T und P&amp;A ersetzt. |
| Integration von Legacy [!DNL Audience Manager] (AAM) in [!DNL Target] | Hierbei handelte es sich um die Integration, die Frontend-API-Aufrufe tätigte, um AAM-Segmente abzurufen, und diese anschließend als Mbox-Parameter bei jedem Mbox-Aufruf an die Seite sendete. |

## Drittanbieterintegrationen

| Integration | Details |
|--- |--- |
| Andere Tag-Manager | „at.js“ sollte auch mit anderen Tag-Management-plattformen funktionieren, die nicht von Adobe stammen, grundsätzlich sollten Sie beim Einsatz benutzerdefinierter Integrationsfunktionen, die von anderen Anbietern entwickelt wurden, jedoch vorsichtig sein. Deren Integrationen sind möglicherweise von internen mbox.js-Funktionen abhängig, die es in at.js nicht mehr gibt. |
| Drittanbieter für Daten (z. B. Demandbase, BlueKai, Wetter-APIs) | Viele Drittanbieter-Datenanbieter, die zur Ergänzung der Target-Benutzerprofilerstellung verwendet werden, können mit der Funktion at.js [Datenanbieter](../atjs-functions/targetglobalsettings.md#data-providers) integriert werden. |
