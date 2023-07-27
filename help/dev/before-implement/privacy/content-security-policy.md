---
keywords: Inhaltssicherheitsrichtlinie, CSP, at.js, Whitelist, Zulassungsliste, Flackern, Vorab-Ausblenden, Vorab-Ausblenden, Vorab-Ausblenden, Inhaltssicherheitsrichtlinie, iFrame, iFrame
description: Erfahren Sie mehr über die CSP-Anweisungen (Content Security Policy), die Sie bei Verwendung von [!DNL Adobe Target].
title: Wie handhabt  [!DNL Target]  Content Security Policies (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 29%

---

# Richtlinien zur Content Security Policy (CSP)

Wenn Sie die [Inhaltssicherheitsrichtlinie](https://de.wikipedia.org/wiki/Content_Security_Policy) (CSP) für [!DNL Adobe Target] -Implementierung sollten Sie bei Verwendung von die folgenden CSP-Anweisungen hinzufügen [at.js 2.1 oder höher](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` mit `*.tt.omtrdc.net` auf der Zulassungsliste. Erforderlich, um die Netzwerkanfrage an das [!DNL Target]-Edge-Netzwerk zuzulassen.
* `style-src unsafe-inline`. Erforderlich, um die Flimmerregelung vorab auszublenden.
* `script-src unsafe-inline`. Erforderlich, um die Ausführung von JavaScript zu ermöglichen, die Teil eines HTML-Angebots sein kann.

## Häufig gestellte Fragen (FAQs)

Wenn Sie Näheres zu Sicherheitsrichtlinien erfahren möchten, lesen Sie die folgenden häufig gestellten Fragen:

### Stellen Cross Origin Resource Sharing- (CORS) und Flash Cross-Domain-Richtlinien Sicherheitsprobleme dar?

Die empfohlene Methode zur Implementierung der CORS-Richtlinie besteht darin, den Zugriff nur auf vertrauenswürdige Quellen zu ermöglichen, die den Zugriff über eine Zulassungsliste mit vertrauenswürdigen Domains verlangen. Dasselbe gilt für die Flash Cross-Domain-Richtlinie. Einige [!DNL Target] -Kunden sind besorgt über die Verwendung von Platzhalterzeichen für Domänen in Target. Wenn ein Benutzer in einer Anwendung angemeldet ist und eine von der Richtlinie zugelassene Domäne besucht, besteht das Problem darin, dass schädliche Inhalte, die in dieser Domäne ausgeführt werden, potenziell sensible Inhalte aus der Anwendung abrufen und Aktionen im Sicherheitskontext des angemeldeten Benutzers ausführen können. Diese Situation wird häufig als CSRF (Cross-Site Request Forgery) bezeichnet.

In [!DNL Target] Diese Maßnahmen sollten jedoch kein Sicherheitsproblem darstellen.

„adobe.tt.omtrdc.net“ ist eine Adobe-eigene Domain. [!DNL Adobe Target] ist ein Test- und Personalisierungs-Tool, und normalerweise kann [!DNL Target] Anfragen von überall empfangen und verarbeiten, ohne dass eine Authentifizierung erforderlich ist. Diese Anfragen enthalten Schlüssel-Wert-Paare, die für A/B-Tests, Empfehlungen oder die Personalisierung von Inhalten verwendet werden.

Adobe speichert keine personenbezogenen Daten (PII) oder andere vertrauliche Informationen über [!DNL Adobe Target] Edge-Server, auf die &quot;adobe.tt.omtrdc.net&quot;verweist.

[!DNL Target] kann von jeder Domain über JavaScript-Aufrufe aufgerufen werden. Die einzige Möglichkeit, diesen Zugriff zu ermöglichen, besteht darin, &quot;Access-Control-Allow-Origin&quot;mit einem Platzhalter zu verwenden.

### Wie lässt sich verhindern, dass meine Site als iFrame unter ausländischen Domänen eingebettet wird?

So lassen Sie [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC) Um Ihre Website in einen iFrame einzubetten, muss die CSP (sofern festgelegt) in Ihrer Webserver-Einstellung geändert werden. [!DNL Adobe] -Domänen müssen auf der Whitelist stehen und konfiguriert werden.

Aus Sicherheitsgründen möchten Sie möglicherweise verhindern, dass Ihre Site als iFrame unter ausländischen Domänen eingebettet wird.

In den folgenden Abschnitten wird erläutert, wie Sie zulassen oder verhindern können, dass VEC Ihre Site in einen iFrame einbettet.

#### Einbetten Ihrer Site in einen iFrame durch VEC zulassen

Die einfachste Lösung, mit der VEC Ihre Website in einen iFrame einbetten kann, besteht darin, die `*.adobe.com`, der größte Platzhalter.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):


![CSP mit dem breitesten Platzhalter](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Möglicherweise möchten Sie nur die tatsächlichen [!DNL Adobe] -Dienst. Dieses Szenario kann mithilfe von `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):

![CSP mit Experience Cloud-Scoping](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

Der restriktivste Zugriff auf das Konto eines Unternehmens lässt sich mit `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`, wobei `<Client Code>` stellt Ihren spezifischen Clientcode dar.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (klicken Sie zum Vergrößern auf ):

![CSP mit clientcode-Bereich](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Wenn Sie [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implementiert ist, muss sie auch entsperrt sein.
>
>Beispiel:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Verhindern, dass VEC Ihre Site in einen iFrame einbettet

Um zu verhindern, dass VEC Ihre Site in einen iFrame einbettet, können Sie nur &quot;self&quot;verwenden.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'`

Wie in der folgenden Abbildung dargestellt (klicken Sie zum Vergrößern auf ):

![CSP-Fehler](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Die folgende Fehlermeldung wird angezeigt:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

