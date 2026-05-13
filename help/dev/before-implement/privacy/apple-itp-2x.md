---
keywords: Apple, ITP, Intelligent Tracking Prevention, Experience Cloud ID, ECID, ITP
description: Erfahren Sie mehr über  [!DNL Adobe Target]  und die Auswirkungen der ITP-Initiative (Intelligent Tracking Prevention) von Apple, die die Privatsphäre von Safari-Benutzern schützen soll.
title: Wie  [!DNL Target]  Apple ITP-Unterstützung?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
TQID: https://experienceleague.adobe.com/AvrlwiLa-soHwrGT1QMa8KgsiIwfwKaF-0LBxMjb8cs
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 681
ht-degree: 28%

---

# Apple Intelligent Tracking Prevention (ITP) 2.x

Intelligent Tracking Prevention (ITP) ist die Initiative von Apple zum Schutz der Privatsphäre von Safari-Benutzern. Die erste Version von ITP, die im Jahr 2017 veröffentlicht wurde, zielte auf die Verwendung von Drittanbieter-Cookies ab. Genau genommen blockierte Apple alle Drittanbieter-Cookies, was wiederum die Arbeit von Anzeigen- und Werbefirmen erschwerte, da Drittanbieter-Cookies allgemein zum Tracking von Besuchern und zur Erfassung von Besucherdaten eingesetzt werden. Jetzt ist Apple dabei, die Verwendung von Erstanbieter-Cookies in Safari zu beschränken.

Die unten angegebenen ITP-Versionen beinhalten die folgenden Einschränkungen:

| Version | Details |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | Clientseitige Cookies, die im Browser mit der `document.cookie` API gesetzt werden, laufen nach sieben Tagen ab.<br />Veröffentlicht am 21. Februar 2019. |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | Der Verfall nach sieben Tagen wurde drastisch auf einen Tag reduziert.<br />Veröffentlicht am Mittwoch, 24. April 2019. |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | Beseitigt mehrere Problemumgehungen, z. B. die Verwendung von localStorage oder die Verwendung der JavaScript `Document.referrer property`.<br />Veröffentlicht am 23. September 2019.<br />CNAME-Cloaking Defense-Funktion zu ITP, veröffentlicht in Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 und iPadOS 14. Alle Cookies, die von einer durch CNAME getarnten HTTP-Antwort eines Drittanbieters erstellt werden, laufen in sieben Tagen ab.<br />Ankündigung vom 12. November 2020. |

## Welche Auswirkungen hat dies für mich als [!DNL Target]?

Target stellt Ihnen JavaScript-Bibliotheken zur Verfügung, die Sie auf Ihren Seiten bereitstellen können, damit [!DNL Target] Ihren Besuchern Echtzeit-Personalisierung bieten können. Es gibt drei [!DNL Target] JavaScript-Bibliotheken at.js 1.*x*, at.js 2.*x*, die [!DNL Adobe Experience Cloud Web SDK], die Client-seitige [!DNL Target]-Cookies über die `document.cookie`-API in den Browsern Ihrer Besucher platzieren. Daher sind [!DNL Target] Cookies von Apples ITP 2.1, 2.2 und 2.3 betroffen und laufen nach sieben Tagen (mit ITP 2.1) und nach einem Tag (mit ITP 2.2 und ITP 2.3) ab.

Apple ITP 2.x wirkt sich auf [!DNL Target] in den folgenden Bereichen aus:

| Wirkung | Details |
| --- | --- |
| Mögliche Zunahme von Unique Visitors | Da das Ablauffenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) eingestellt ist, kann es zu einem Anstieg der Unique Visitors kommen, die von Safari-Browsern kommen. Wenn Ihre Besucher nach sieben Tagen (ITP 2.1) oder einem Tag (ITP 2.2 und ITP 2.3) erneut Ihre Domain aufrufen, ist [!DNL Target] gezwungen, anstelle des abgelaufenen Cookies ein neues [!DNL Target]-Cookie in Ihrer Domain zu setzen. Das neue [!DNL Target]-Cookie wird als neuer Unique Visitor gewertet, auch wenn der Benutzer derselbe ist. |
| Verringerte Lookback-Zeiträume für [!DNL Target]-Aktivitäten | Besucherprofile für [!DNL Target]-Aktivitäten haben möglicherweise für die Entscheidungsfindung einen verringerten Lookback-Zeitraum. [!DNL Target]-Cookies werden verwendet, um einen Besucher zu erkennen und Benutzerprofilattribute zur Personalisierung zu speichern. Da [!DNL Target] Cookies in Safari nach sieben Tagen (ITP 2.1) oder einem Tag (ITP 2.2 und 2.3) abgelaufen sein können, können die Benutzerprofildaten, die mit dem bereinigten [!DNL Target]-Cookie verknüpft waren, nicht für die Entscheidungsfindung verwendet werden. |
| Profil-Skripte, die auf der ID von Drittanbietern (3rdPartyID) basieren | Da das Gültigkeitsfenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) festgelegt wird, funktionieren [Profilskripte](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=de) die auf dem 3rdPartyID-Cookie basieren, nach Ablauf nicht mehr. |
| QA-/Vorschau-URLs auf iOS-Geräten | Da das Gültigkeitsfenster auf sieben Tage (mit ITP 2.1) und einen Tag (mit ITP 2.2 und ITP 2.3) festgelegt wird, funktionieren [QA-/Vorschau-URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html?lang=de) nach Ablauf nicht mehr, da die URLs auf dem ThirdPartyID-Cookie basieren. |

## Ist meine aktuelle [!DNL Target]-Implementierung betroffen?

Wenn Sie die Experience Cloud ID-Bibliothek (ECID-Bibliothek) zusätzlich zur [!DNL Target] JavaScript-Bibliothek verwenden, wird Ihre Implementierung auf die in diesem Artikel aufgeführten Arten beeinflusst: [Auswirkungen von Safari ITP 2.1 auf Adobe Experience Cloud- und Experience Platform-Kunden](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
