---
keywords: benutzerspezifische Ereignisse, at.js, Anforderung fehlgeschlagen, Anfrage erfolgreich, Inhaltswiedergabe fehlgeschlagen, Inhaltswiedergabe erfolgreich, Bibliothek geladen, Anforderungsstart, Start des Inhalts-Renderings, Inhaltswiedergabe ohne Angebote, Inhaltswiedergabe, Umleitung, benutzerspezifische Ereignisse2
description: Verwenden Sie benutzerspezifische Ereignisse für die JavaScript-Bibliothek [!DNL Adobe Target] at.js , um benachrichtigt zu werden, wenn eine Mbox-Anforderung oder ein Angebot erfolgreich war oder fehlgeschlagen ist.
title: Wie verwende ich benutzerdefinierte at.js-Ereignisse?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 71%

---

# Benutzerdefinierte at.js-Ereignisse

Informationen zu `at.js custom events`, die Sie darüber informieren, ob eine Mbox-Anforderung oder ein Angebot erfolgreich war oder fehlgeschlagen ist.

In der Vergangenheit ließ mbox.js (jetzt nicht mehr unterstützt) anderen JavaScript-Code, der auf der Seite ausgeführt wird, nicht wissen, was hinter den Kulissen geschieht. Dank der Weiterentwicklung von at.js konnten wir dieses Problem glücklicherweise beheben.

Laut unseren Kunden gibt es mehrere Szenarien, über die sie gerne informiert werden möchten, darunter:

* Fehlschlagen einer Mbox-Abfrage aufgrund einer Zeitüberschreitung, des falschen Status-Codes, eines JSON-Parsingfehlers usw.
* Erfolg einer Mbox-Abfrage
* Fehlschlagen der Wiedergabe eines Angebots aufgrund eines fehlenden Wrapper-Mbox-Elements, eines nicht gefundenen Selektors usw.
* Erfolg der Angebotswiedergabe. Anwendung von DOM-Änderungen.

Vordefinierte Ereignisse mit einer Struktur, die die Extrahierung von erforderlichen Daten je nach Ereignistyp ermöglicht

Sicherstellung, dass Ereignisse in verschiedenen Szenarien eingesetzt werden können, benutzerdefinierte Ereignisse über ein Nutzlastobjekt verfügen, das der Detaileinheit des Ereignisobjekts zugeordnet ist (und an den Handler übermittelt wird). Des Weiteren auch das Verhindern der Übermittlung von Zeichenfolgen wie Ereignisnamen. Die Ereignisse werden mithilfe des `adobe.target.event`-Namespace als Konstanten dargestellt.

## Struktur

| Schlüssel | Typ | Beschreibung |
|--- |--- |--- |
| Typ | Zeichenfolge | Es gibt verschiedene Szenarien, in denen Sie über die Unterstützung in Bezug auf die Ablaufverfolgungs-, Debugging- und Anpassungsinteraktionen mit at.js benachrichtigt werden möchten.<p>Jedes im Folgenden aufgeführte benutzerspezifische Ereignis besitzt zwei Formate: eine „Konstante“ und einen „Zeichenfolgenwert“.<ul><li>**Konstante:** `adobe.target.event.` vorangestellt, in Großbuchstaben dargestellt, enthalten Unterstriche. Verwenden Sie die Konstante, um benutzerspezifische Ereignisse zu abonnieren, *nachdem* at.js geladen, jedoch *bevor* die Mbox-Antwort empfangen wurde.</li><li>**Zeichenfolgenwerte:** Kleinbuchstaben, enthalten Gedankenstriche. Verwenden Sie den Zeichenfolgenwert, um benutzerspezifische Ereignisse zu abonnieren, *bevor* at.js geladen wird.</li></ul>**Anforderung fehlgeschlagen**<p>Konstante: `adobe.target.event.REQUEST_FAILED`<p>Zeichenfolgenwert: `at-request-failed`<p>Beschreibung: Eine Mbox-Anfrage schlägt aufgrund eines Timeouts, eines falschen Status-Codes, eines JSON-Analysefehlers usw. fehl.<p>**Anfrage erfolgreich**<p>Konstante: `adobe.target.event.REQUEST_SUCCEEDED`<p>Zeichenfolgenwert: `at-request-succeeded`<p>Beschreibung: Eine Mbox-Anfrage war erfolgreich.<p>**Inhaltsdarstellung fehlgeschlagen**<p>Konstante: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>Zeichenfolgenwert: `at-content-rendering-failed`<p>Beschreibung: Die Angebotsdarstellung schlug fehl, weil ein Mbox-Umbruchselement fehlt, die Auswahl nicht gefunden werden kann usw.<p>**Inhaltsdarstellung erfolgreich**<p>Konstante: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>Zeichenfolgenwert: `at-content-rendering-succeeded`<p>Beschreibung: Die Angebotsdarstellung war erfolgreich. Anwendung von DOM-Änderungen.<p>**Bibliothek geladen**<p>Konstante: `adobe.target.event.LIBRARY_LOADED`<p>Zeichenfolgenwert: `at-library-loaded`<p>Beschreibung: Dieses Ereignis ist ideal geeignet, um nachzuverfolgen, wann at.js vollständig geladen wurde. Mit diesem Ereignis können Sie die Ausführung der globalen Mbox anpassen. Sie können dieses Ereignis auch verwenden, um die globale Mbox zu deaktivieren und dieses Ereignis anschließend zu überwachen, um die globale Mbox später auszulösen.<p>**Start der Anfrage**<p>Konstante: `adobe.target.event.REQUEST_START`<p>Zeichenfolgenwert: `at-request-start`<p>Beschreibung: Dieses Ereignis wird ausgelöst, bevor eine HTTP-Anfrage ausgeführt wird. Sie können dieses Ereignis für Leistungsmessungen mit der Resource Timing-API verwenden.<p>**Start der Inhaltsdarstellung**<p>Konstante: `adobe.target.event.CONTENT_RENDERING_START`<p>Zeichenfolgenwert: `at-content-rendering-start`<p>Beschreibung: Dieses Ereignis wird ausgelöst, bevor das Selektor-Polling gestartet und der Inhalt auf der Seite dargestellt wird. Sie können dieses Ereignis verwenden, um den Inhaltsdarstellungsfortschritt nachzuverfolgen.<p>**Inhaltsdarstellung - keine Angebote**<p>Konstante: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>Zeichenfolgenwert: `at-content-rendering-no-offers`<p>Beschreibung: Dieses Ereignis wird ausgelöst, wenn keine Angebote zurückgegeben werden.<p>**Umleitung der Inhaltsdarstellung**<p>Konstante: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>Zeichenfolgenwert: `at-content-rendering-redirect`<p>Beschreibung: Dieses Ereignis wird ausgelöst, wenn ein Angebot eine Umleitung ist und [!DNL Target] zu einer anderen URL umleitet. |
| mbox | Zeichenfolge | Name der Mbox |
| message | Zeichenfolge | Enthält für Menschen lesbare Beschreibungen, beispielsweise zu Geschehnissen, zur Fehlermeldung usw. |
| Verfolgung | Objekt | Enthält `sessionId` und `deviceId`. In einigen Fällen fehlt die `deviceId` möglicherweise, weil [!DNL Target] sie nicht vom Edge-Server abrufen konnte. |
| Typ | Zeichenfolge | **Entscheidungsartefakt auf Gerät erfolgreich**<p>Konstante:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>Zeichenfolgenwert: `artifactDownloadSucceeded`<p>Beschreibung: Wird aufgerufen, wenn das auf dem Gerät bereitgestellte Entscheidungsartefakt erfolgreich heruntergeladen wurde.<p>**Entscheidungsartefakt auf dem Gerät fehlgeschlagen**<p>Konstante: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>Zeichenfolgenwert: `artifactDownloadFailed`<p>Beschreibung: Wird aufgerufen, wenn das on-device Decisioning-Artefakt nicht heruntergeladen werden konnte. |

## Nutzung

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Schulungsvideo: Antwort-Token und der benutzerdefinierte at.js-Ereignisse ![Tutorial-Badge](../../../assets/tutorial.png)

Sehen Sie sich das folgende Video an, um zu erfahren, wie Sie mithilfe von Antwort-Token und benutzerspezifischen at.js-Ereignissen Profilinformationen von [!DNL Target] an Drittanbietersysteme weitergeben können.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
