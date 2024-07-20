---
keywords: Inhaltssicherheitsrichtlinie, CSP, at.js, Whitelist, Zulassungsliste, Flackern, Vorab-Ausblenden, Vorab-Ausblenden, Vorab-Ausblenden, Inhaltssicherheitsrichtlinie, iFrame, iFrame
description: Erfahren Sie mehr über die CSP-Anweisungen (Content Security Policy), die Sie bei Verwendung von  [!DNL Adobe Target] hinzufügen sollten.
title: Wie handhabt  [!DNL Target]  Content Security Policies (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# Richtlinien zur Content Security Policy (CSP)

Wenn Sie die [Content Security Policy](https://de.wikipedia.org/wiki/Content_Security_Policy) (CSP) für Ihre [!DNL Adobe Target] -Implementierung verwenden, sollten Sie die folgenden CSP-Anweisungen hinzufügen, wenn Sie [at.js 2.1 oder höher](../../implement/client-side/atjs/target-atjs-versions.md) verwenden:

* `connect-src` mit `*.tt.omtrdc.net` auf der Zulassungsliste. Erforderlich, um die Netzwerkanfrage an das [!DNL Target]-Edge-Netzwerk zuzulassen.
* `style-src unsafe-inline`. Erforderlich, um die Flimmerregelung vorab auszublenden.
* `script-src unsafe-inline`. Erforderlich, um die Ausführung von JavaScript zu ermöglichen, die Teil eines HTML-Angebots sein kann.

## Häufig gestellte Fragen (FAQs)

Wenn Sie Näheres zu Sicherheitsrichtlinien erfahren möchten, lesen Sie die folgenden häufig gestellten Fragen:

### Stellen Cross Origin Resource Sharing- (CORS) und Flash Cross-Domain-Richtlinien Sicherheitsprobleme dar?

Die empfohlene Methode zur Implementierung der CORS-Richtlinie besteht darin, den Zugriff nur auf vertrauenswürdige Quellen zu ermöglichen, die den Zugriff über eine Zulassungsliste mit vertrauenswürdigen Domains verlangen. Dasselbe gilt für die Flash Cross-Domain-Richtlinie. Einige [!DNL Target] -Kunden sind besorgt über die Verwendung von Platzhalterzeichen für Domänen in Target. Wenn ein Benutzer in einer Anwendung angemeldet ist und eine von der Richtlinie zugelassene Domäne besucht, besteht das Problem darin, dass schädliche Inhalte, die in dieser Domäne ausgeführt werden, potenziell sensible Inhalte aus der Anwendung abrufen und Aktionen im Sicherheitskontext des angemeldeten Benutzers ausführen können. Diese Situation wird häufig als CSRF (Cross-Site Request Forgery) bezeichnet.

Bei einer Implementierung von [!DNL Target] sollten diese Richtlinien jedoch kein Sicherheitsproblem darstellen.

„adobe.tt.omtrdc.net“ ist eine Adobe-eigene Domain. [!DNL Adobe Target] ist ein Test- und Personalisierungs-Tool, und normalerweise kann [!DNL Target] Anfragen von überall empfangen und verarbeiten, ohne dass eine Authentifizierung erforderlich ist. Diese Anfragen enthalten Schlüssel-Wert-Paare, die für A/B-Tests, Empfehlungen oder die Personalisierung von Inhalten verwendet werden.

Adobe speichert keine personenbezogenen oder anderen sensiblen Informationen (PII) oder andere vertrauliche Informationen auf [!DNL Adobe Target] -Edge-Servern, auf die &quot;adobe.tt.omtrdc.net&quot;verweist.

[!DNL Target] kann von jeder Domain über JavaScript-Aufrufe aufgerufen werden. Die einzige Möglichkeit, diesen Zugriff zu ermöglichen, besteht darin, &quot;Access-Control-Allow-Origin&quot;mit einem Platzhalter zu verwenden.

### Wie lässt sich verhindern, dass meine Site als iFrame unter ausländischen Domänen eingebettet wird?

Damit der [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) Ihre Website in einen iFrame einbetten kann, muss die CSP (sofern festgelegt) in Ihrer Webservereinstellung geändert werden. [!DNL Adobe] -Domänen müssen auf der Whitelist stehen und konfiguriert werden.

Aus Sicherheitsgründen möchten Sie möglicherweise verhindern, dass Ihre Site als iFrame unter ausländischen Domänen eingebettet wird.

In den folgenden Abschnitten wird erläutert, wie Sie zulassen oder verhindern können, dass VEC Ihre Site in einen iFrame einbettet.

#### Einbetten Ihrer Site in einen iFrame durch VEC zulassen

Die einfachste Lösung, mit der VEC Ihre Website in einen iFrame einbetten kann, besteht darin, `*.adobe.com` zuzulassen, den größten Platzhalter.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):


![CSP mit dem größten Platzhalter](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Möglicherweise möchten Sie nur den tatsächlichen [!DNL Adobe] -Dienst zulassen. Dieses Szenario kann mit `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com` erreicht werden.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):

![CSP mit Experience Cloud-Scoped](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

Der restriktivste Zugriff auf das Konto eines Unternehmens kann mit `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com` erzielt werden, wobei `<Client Code>` für Ihren spezifischen Clientcode steht.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):

![CSP mit clientcode-Bereich](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Wenn Sie [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implementiert haben, muss auch die Sperre aufgehoben werden.
>
>Beispiel:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Verhindern, dass VEC Ihre Site in einen iFrame einbettet

Um zu verhindern, dass VEC Ihre Site in einen iFrame einbettet, können Sie nur &quot;self&quot;verwenden.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'`

Wie in der folgenden Abbildung dargestellt (klicken Sie zum Vergrößern auf ):

![CSP error](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Die folgende Fehlermeldung wird angezeigt:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

