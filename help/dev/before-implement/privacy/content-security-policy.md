---
keywords: auf die Zulassungsliste setzen Content Security Policy, CSP, at.js, Whitelist, Flackern, pre-hide, pre-hiding, Prehiding, Content Security Policy, iFrame, iFrame
description: Erfahren Sie mehr über die CSP-Richtlinien (Content Security Policy), die Sie bei Verwendung von hinzufügen sollten [!DNL Adobe Target].
title: Wie handhabt  [!DNL Target]  Content Security Policies (CSP)?
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# Richtlinien zur Content Security Policy (CSP)

Wenn Sie die [Content Security Policy](https://de.wikipedia.org/wiki/Content_Security_Policy) (CSP) für Ihre [!DNL Adobe Target]-Implementierung verwenden, sollten Sie die folgenden CSP-Anweisungen hinzufügen, wenn Sie at.[ 2.1 oder höher verwenden](../../implement/client-side/atjs/target-atjs-versions.md):

* `connect-src` mit `*.tt.omtrdc.net` auf der Zulassungsliste. Erforderlich, um die Netzwerkanfrage an das [!DNL Target]-Edge-Netzwerk zuzulassen.
* `style-src unsafe-inline`. Erforderlich, um die Flimmerregelung vorab auszublenden.
* `script-src unsafe-inline`. Erforderlich, um die Ausführung von JavaScript zu ermöglichen, die Teil eines HTML-Angebots sein kann.

## Häufig gestellte Fragen (FAQs)

Wenn Sie Näheres zu Sicherheitsrichtlinien erfahren möchten, lesen Sie die folgenden häufig gestellten Fragen:

### Stellen Cross Origin Resource Sharing- (CORS) und Flash Cross-Domain-Richtlinien Sicherheitsprobleme dar?

Die empfohlene Methode zur Implementierung der CORS-Richtlinie besteht darin, den Zugriff nur auf vertrauenswürdige Quellen zu ermöglichen, die den Zugriff über eine Zulassungsliste mit vertrauenswürdigen Domains verlangen. Dasselbe gilt für die Flash Cross-Domain-Richtlinie. Einige [!DNL Target]-Kunden sind besorgt über die Verwendung von Platzhalterzeichen für Domains in Target. Problematisch ist Folgendes: Wenn ein Benutzer bei einer Anwendung angemeldet ist und eine von der Richtlinie zugelassene Domain besucht, können schädliche Inhalte, die in dieser Domain ausgeführt werden, möglicherweise sensible Inhalte aus der Anwendung abrufen und Aktionen im Sicherheitskontext des angemeldeten Benutzers ausführen. Diese Situation wird häufig als Cross-Site Request Forgery (CSRF) bezeichnet.

In einer [!DNL Target] Implementierung stellen diese Richtlinien jedoch kein Sicherheitsproblem dar.

„adobe.tt.omtrdc.net“ ist eine Adobe-eigene Domain. [!DNL Adobe Target] ist ein Test- und Personalisierungs-Tool, und normalerweise kann [!DNL Target] Anfragen von überall empfangen und verarbeiten, ohne dass eine Authentifizierung erforderlich ist. Diese Anfragen enthalten Schlüssel-Wert-Paare, die für A/B-Tests, Empfehlungen oder die Personalisierung von Inhalten verwendet werden.

Adobe speichert keine personenbezogenen oder anderen sensiblen Informationen auf [!DNL Adobe Target] Edge-Servern, auf die &quot;adobe.tt.omtrdc.net“ verweist.

[!DNL Target] kann von jeder Domain über JavaScript-Aufrufe aufgerufen werden. Die einzige Möglichkeit, diesen Zugriff zuzulassen, besteht darin, „Access-Control-Allow-Origin“ mit einem Platzhalter anzuwenden.

### Wie kann ich zulassen oder verhindern, dass meine Website als iFrame unter fremden Domains eingebettet wird?

Damit der [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=de){target=_blank} (VEC) Ihre Website in einen iFrame einbetten kann, muss die CSP (falls festgelegt) in der Webservereinstellung geändert werden. [!DNL Adobe]-Domains müssen auf die Whitelist gesetzt und konfiguriert werden.

Aus Sicherheitsgründen möchten Sie möglicherweise verhindern, dass Ihre Site als iFrame unter fremden Domains eingebettet wird.

In den folgenden Abschnitten wird erläutert, wie Sie das Einbetten Ihrer Site in einen iFrame durch VEC zulassen oder verhindern können.

#### Zulassen, dass VEC Ihre Site in einen iFrame einbettet

Die einfachste Lösung, mit der VEC Ihre Website in einen iFrame einbetten kann, besteht darin, `*.adobe.com` zuzulassen, wobei es sich um den breitesten Platzhalter handelt.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

Wie in der folgenden Abbildung (zum Vergrößern klicken):


![CSP mit dem breitesten Platzhalter](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

Möglicherweise möchten Sie nur den tatsächlichen [!DNL Adobe]-Service zulassen. Dieses Szenario kann mithilfe von `*.experiencecloud.adobe.com + https://experiencecloud.adobe.com` erreicht werden.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (zum Vergrößern klicken):

![CSP mit Experience Cloud-Umfang](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

Der restriktivste Zugriff auf das Konto eines Unternehmens kann mithilfe von `https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com` erzielt werden, wobei `<Client Code>` Ihren spezifischen Client-Code darstellt.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

Wie in der folgenden Abbildung (zum Vergrößern klicken):

![CSP mit Clientcode-Bereich](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Wenn Sie [Launch/Tag](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) implementiert haben, muss diese ebenfalls entsperrt werden.
>
>Beispiel:
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### Verhindern, dass VEC Ihre Site in einen iFrame einbettet

Um zu verhindern, dass VEC Ihre Site in einen iFrame einbettet, können Sie auf „sich selbst“ beschränken.

Beispiel:

`Content-Security-Policy: frame-ancestors 'self'`

Wie in der folgenden Abbildung dargestellt (zum Vergrößern klicken):

![CSP-Fehler](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

Die folgende Fehlermeldung wird angezeigt:

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

