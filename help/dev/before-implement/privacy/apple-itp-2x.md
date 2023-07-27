---
keywords: Apple, ITP, Intelligent Tracking Prevention, Experience Cloud ID, ecid, itp
description: Informationen zu [!DNL Adobe Target] und die Auswirkungen der Initiative Apple Intelligent Tracking Prevention (ITP) zum Schutz der Privatsphäre von Safari-Benutzern.
title: Funktionsweise [!DNL Target] Apple ITP-Support handhaben?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 32%

---

# Apple Intelligent Tracking Prevention (ITP) 2.x

Intelligent Tracking Prevention (ITP) ist die Apple-Initiative zum Schutz der Privatsphäre von Safari-Benutzern. Die erste Version von ITP, die im Jahr 2017 veröffentlicht wurde, zielte auf die Verwendung von Drittanbieter-Cookies ab. Genau genommen blockierte Apple alle Drittanbieter-Cookies, was wiederum die Arbeit von Anzeigen- und Werbefirmen erschwerte, da Drittanbieter-Cookies allgemein zum Tracking von Besuchern und zur Erfassung von Besucherdaten eingesetzt werden. Jetzt ist Apple dabei, die Verwendung von Erstanbieter-Cookies in Safari zu beschränken.

Die unten angegebenen ITP-Versionen beinhalten die folgenden Einschränkungen:

| Version | Details |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Clientseitige Cookies, die im Browser mit der `document.cookie` API gesetzt werden, laufen nach sieben Tagen ab.<br />Veröffentlicht am 21. Februar 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Der Verfall nach sieben Tagen wurde drastisch auf einen Tag reduziert.<br />Veröffentlicht am Mittwoch, 24. April 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-3-2/) | Mehrere Problemumgehungen wurden beseitigt, z. B. die Verwendung von localStorage oder die Verwendung von JavaScript `Document.referrer property`.<br />Veröffentlicht am 23. September 2019.<br />CNAME-Cloaking-Verteidigungsfunktion für ITP, die in Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 und iPadOS 14 veröffentlicht wurde. Alle Cookies, die von einer CNAME-blockierten HTTP-Antwort eines Drittanbieters erstellt werden, laufen in sieben Tagen ab.<br />Angesagt am 12. November 2020. |

## Wie wirkt sich dies auf mich als [!DNL Target] Kunde?

Target stellt Ihnen JavaScript-Bibliotheken zur Verfügung, die Sie auf Ihren Seiten bereitstellen können, damit [!DNL Target] Sie können Ihren Besuchern eine Echtzeit-Personalisierung bereitstellen. Es gibt drei [!DNL Target] JavaScript-Bibliotheken at.js 1.*x*, at.js 2.*x*, die [!DNL Adobe Experience Cloud Web SDK] die Client-seitig platzieren [!DNL Target] Cookies in den Browsern Ihrer Besucher über die `document.cookie` API. Daher [!DNL Target] -Cookies sind von ITP 2.1, 2.2 und 2.3 von Apple betroffen und laufen nach sieben Tagen (mit ITP 2.1) und nach einem Tag (mit ITP 2.2 und ITP 2.3) ab.

Auswirkungen von Apple ITP 2.x [!DNL Target] in den folgenden Bereichen:

| Wirkung | Details |
| --- | --- |
| Mögliche Zunahme von Unique Visitors | Da das Ablauffenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) festgelegt ist, kann es zu einem Anstieg der Unique Visitors kommen, die von Safari-Browsern stammen. Wenn Ihre Besucher Ihre Domäne nach sieben Tagen (ITP 2.1) oder einem Tag (ITP 2.2 und ITP 2.3) erneut aufrufen, [!DNL Target] wird gezwungen, einen neuen [!DNL Target] -Cookie in Ihrer Domäne anstelle des abgelaufenen Cookies. Das neue [!DNL Target]-Cookie wird als neuer Unique Visitor gewertet, auch wenn der Benutzer derselbe ist. |
| Verringerte Lookback-Zeiträume für [!DNL Target]-Aktivitäten | Besucherprofile für [!DNL Target]-Aktivitäten haben möglicherweise für die Entscheidungsfindung einen verringerten Lookback-Zeitraum. [!DNL Target]-Cookies werden verwendet, um einen Besucher zu erkennen und Benutzerprofilattribute zur Personalisierung zu speichern. Da [!DNL Target] -Cookies können in Safari nach sieben Tagen (ITP 2.1) oder einem Tag (ITP 2.2 und 2.3) abgelaufen sein. Dabei handelt es sich um die Benutzerprofildaten, die mit der Bereinigung verknüpft waren. [!DNL Target] -Cookie kann nicht für die Entscheidungsfindung verwendet werden. |
| Profil-Skripte, die auf der ID von Drittanbietern (3rdPartyID) basieren | Da das Ablauffenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) eingestellt ist, [Profilskripte](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) basierend auf dem 3rdPartyID-Cookie funktioniert nach Ablauf nicht mehr. |
| QA-/Vorschau-URLs auf iOS-Geräten | Da das Ablauffenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) eingestellt ist, [QA-/Vorschau-URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) funktioniert nach Ablauf nicht mehr, da die URLs auf dem 3rdPartyID-Cookie basieren. |

## Ist meine aktuelle [!DNL Target]-Implementierung betroffen?

Wenn Sie die Experience Cloud-ID-Bibliothek (ECID) zusätzlich zur [!DNL Target] JavaScript-Bibliothek verwenden, wird Ihre Implementierung auf die in diesem Artikel aufgeführten Arten beeinträchtigt: [Auswirkungen von Safari ITP 2.1 auf Adobe Experience Cloud und Experience Platform-Kunden](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
