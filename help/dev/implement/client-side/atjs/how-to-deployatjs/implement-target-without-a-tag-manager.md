---
keywords: Target implementieren, Implementierung, at.js implementieren, Tag Manager, On-Device Decisioning, On-Device Decisioning
description: Erfahren Sie, wie Sie die Einstellungen (Kontodetails, Implementierungsmethoden usw.) angeben, um die at. [!DNL Adobe Target] -Bibliothek ohne Verwendung eines Tag-Managers zu implementieren.
title: Kann ich  [!DNL Target]  Tag Manager implementieren?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 35%

---

# Implementieren von [!DNL Target] ohne einen Tag-Manager

Informationen zur Implementierung von [!DNL Adobe Target] ohne einen Tag-Manager oder Tags in [!DNL Adobe Experience Platform].

>[!NOTE]
>
>Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sind die bevorzugte Methode zur Implementierung von [!DNL Target] und der at.js-Bibliothek. Die folgenden Informationen sind bei Verwendung von Tags in [!DNL Adobe Experience Platform] zur Implementierung von [!DNL Target] nicht anwendbar.

Um auf die Seite Implementierung zuzugreifen, klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

Sie können die folgenden Einstellungen auf dieser Seite festlegen:

* Kontodetails
* Implementierungsmethoden
* Profil-API
* Debugger-Tools
* Datenschutz

>[!NOTE]
>
>Sie können Einstellungen in der at.js-Bibliothek überschreiben, anstatt sie in der Benutzeroberfläche von [!DNL Target] Standard/Premium oder durch Verwendung von REST-APIs zu konfigurieren. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Kontodetails

Sie können die folgenden Kontodetails anzeigen. Diese Einstellungen können nicht geändert werden.

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Client Code] | Der Client-Code ist eine Client-spezifische Zeichenfolge, die bei der Verwendung der [!DNL Target]-APIs häufig erforderlich ist. |
| [!UICONTROL IMS Organization ID] | Diese ID verknüpft Ihre Implementierung mit Ihrem Adobe Experience Cloud-Konto. |
| [!UICONTROL On-Device Decisioning] | Um die geräteinterne Entscheidungsfindung zu aktivieren, schieben Sie den Umschalter auf die Position „ein“.<p>Die geräteinterne Entscheidungsfindung ermöglicht es Ihnen, Ihre A/B- und Experience Targeting(XT)-Kampagnen auf Ihrem Server zwischenzuspeichern und speicherinterne Entscheidungen mit einer Latenz von nahezu null durchzuführen. Weitere Informationen finden Sie [Einführung in die geräteinterne Entscheidungsfindung](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | (Bedingt) Diese Option wird angezeigt, wenn Sie die geräteinterne Entscheidungsfindung aktivieren.<p>Schieben Sie den Umschalter auf die Position „Ein“, wenn alle Ihre Live [!DNL Target]-Aktivitäten, die für die Entscheidungsfindung auf dem Gerät qualifiziert sind, automatisch in das Artefakt aufgenommen werden sollen.<p>Wenn Sie diesen Umschalter deaktiviert lassen, müssen Sie alle Entscheidungsaktivitäten auf dem Gerät neu erstellen und aktivieren, damit sie in das generierte Regelartefakt aufgenommen werden. |

## Implementierungsmethoden

Die folgenden Einstellungen können im Bedienfeld Implementierungsmethoden konfiguriert werden:

### Globale Einstellungen

>[!NOTE]
>
>Diese Einstellungen werden auf alle [!DNL Target] JS-Bibliotheken angewendet. Nachdem Sie Änderungen im Abschnitt Implementierungsmethoden vorgenommen haben, müssen Sie die Bibliothek herunterladen und in Ihrer Implementierung aktualisieren.

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | Wählen Sie aus, ob der globale Mbox-Aufruf in die Datei at.js integriert werden soll, damit er automatisch bei jedem Laden der Seite aktiviert wird. |
| [!UICONTROL Global mbox] | Wählen Sie einen Namen für die globale Mbox aus. Der Standardname lautet target-global-mbox.<p>Sonderzeichen wie kaufmännische Und-Zeichen (&amp;) können in Mbox-Namen mit at.js verwendet werden. |
| [!UICONTROL Timeout (seconds)] | Falls [!DNL Target] nicht innerhalb des festgelegten Zeitraums mit Inhalten antwortet, erfolgt ein Timeout für den Server-Aufruf und es werden Standardinhalte angezeigt. Während der Sitzung des Besuchers werden weiter Aufrufe durchgeführt. Der Standardwert liegt bei 5 Sekunden.<p>Die at.js-Bibliothek verwendet die Zeitüberschreitungseinstellung in `XMLHttpRequest`. Die maximale Wartezeit beginnt, wenn die Anfrage ausgelöst wird, und endet, wenn [!DNL Target] eine Antwort vom Server erhält. Weitere Informationen finden Sie unter [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout) im Mozilla Developer Network.<p>Wenn die angegebene Zeitüberschreitung vor Erhalt der Antwort eintritt, wird der Standardinhalt angezeigt und der Besucher wird möglicherweise als Teilnehmer einer Aktivität gezählt, da die gesamte Datenerfassung am [!DNL Target] Edge erfolgt. Wenn die Anfrage den [!DNL Target] Edge erreicht, wird der Besucher gezählt.<p>Beim Konfigurieren der Timeout-Einstellung müssen Sie Folgendes beachten:<ul><li>Wenn der Wert zu niedrig ist, erhalten Besucher wahrscheinlich meist nur den Standardinhalt angezeigt, auch wenn sie möglicherweise als Teilnehmer in einer Aktivität gezählt werden.</li><li>Ist der Wert zu hoch, werden Besuchern unter Umständen leere Stellen auf Ihrer Webseite oder komplett leere Seiten angezeigt, falls Sie für längere Zeiträume Textausblendung einsetzen.</li></ul>Genaueres über Mbox-Antwortzeiten erfahren Sie auf der Registerkarte „Netzwerk“ in den Entwicklertools Ihres Browsers. Sie können auch Tools zur Überwachung der Webleistung einsetzen, die von Drittanbietern stammen, wie zum Beispiel Catchpoint.<p>**Hinweis**: Die Einstellung [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) stellt sicher, dass [!DNL Target] nicht zu lange auf die Antwort der Besucher-API wartet. Diese Einstellung und die hier beschriebene Timeout-Einstellung für at.js beeinflussen sich nicht gegenseitig. |
| [!UICONTROL Profile Lifetime] | Mit dieser Einstellung legen Sie fest, wie lange Besucherprofile gespeichert werden. Profile werden standardmäßig zwei Wochen lang gespeichert. Diese Einstellung kann auf 90 Tage erhöht werden.<p>Um die Einstellung für die Profillebensdauer zu ändern, wenden Sie sich an [Kundenunterstützung](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C). |

### Wichtigste Implementierungsmethode

>[!NOTE]
>
>[!DNL Adobe Target] unterstützt sowohl at.js 1.*x* und in at.js 2.*x*. Aktualisieren Sie auf die neueste Version einer der Hauptversionen von at.js, um sicherzustellen, dass Sie eine unterstützte Version ausführen.

Um die gewünschte at.js-Version herunterzuladen, klicken Sie auf die entsprechende Schaltfläche **Herunterladen**.

Um die at.js-Einstellung zu bearbeiten, klicken Sie **[!UICONTROL Edit]** neben der gewünschten at.js-Version.

>[!WARNING]
>
>Bevor Sie diese Standardeinstellungen ändern, wenden Sie sich an [Kundenunterstützung](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C), damit Ihre aktuelle Implementierung nicht beeinträchtigt wird.

Zusätzlich zu den oben erläuterten Einstellungen sind auch die folgenden spezifischen at.js-Einstellungen verfügbar:

| Einstellung | Beschreibung |
|--- |--- |
| Domain-übergreifend | Für at.js v1.*x*, geben Sie an, ob domänenübergreifende Funktionen `disabled` sind (Browser setzen Cookies nur in Ihrer Domain (Erstanbieter-Cookies), `x only` (Browser setzen Cookies nur in der Domain von Target) oder beides, indem Sie `enabled` auswählen (Browser setzen sowohl Erstanbieter- als auch Drittanbieter-Cookies). Geben Sie für at.js v2.10 und höher an, ob domänenübergreifende Funktionen `enabled` (Browser setzen sowohl Cookies von Erstanbietern als auch von Drittanbietern) oder `disabled` (Browser setzen keine Cookies von Drittanbietern) sind. |
| Benutzerdefinierte Bibliothekskopfzeile | Fügen Sie benutzerdefiniertes JavaScript hinzu, das oben in der Bibliothek aufgeführt wird. |
| Benutzerdefinierter Bibliotheksfuß | Fügen Sie benutzerdefiniertes JavaScript hinzu, das unten in der Bibliothek aufgeführt wird. |

### Profil-API

Aktivieren oder deaktivieren Sie die Authentifizierung für Batch-Aktualisierungen via API und generieren Sie ein Token für die Profilauthentifizierung.

Weitere Informationen finden Sie unter [Profil-API-Einstellungen](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### Debugger-Tools

Generieren eines Autorisierungstokens zur Verwendung erweiterter [!DNL Target]-Debugging-Tools Klicken Sie auf **[!UICONTROL Generate New Authentication Token]**.

![Neues Authentifizierungstoken erstellen](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### Datenschutz

Mit diesen Einstellungen können Sie [!DNL Target] in Übereinstimmung mit den geltenden Datenschutzgesetzen verwenden.

Wählen Sie die gewünschte Einstellung aus der Dropdown-Liste Besucher-IP-Adresse verschleiern aus:

* Verschleierung des letzten Oktetts
* Verschleierung der gesamten IP
* Keine

Weitere Informationen finden Sie unter [Datenschutz](/help/dev/before-implement/privacy/privacy.md).

>[!NOTE]
>
>Die Option „Legacy-Browser-Unterstützung“ war in at.js-Version 0.9.3 und früher verfügbar. Diese Option wurde in at.js, Version 0.9.4, entfernt. Eine Liste der von at.js unterstützten Browser finden Sie unter [Unterstützte Browser](/help/dev/before-implement/supported-browsers.md).<p>Bei älteren Browsern handelt es sich in der Regel um alte Versionen, die CORS (Cross Origin Resource Sharing) nicht vollständig unterstützen. Solche Browser sind zum Beispiel alle Versionen von Internet Explorer vor Version 11 oder Safari Version 6 und ältere Versionen. Wenn die Unterstützung älterer Browser deaktiviert war, haben [!DNL Target] in Berichten über diese Browser keine Inhalte bereitgestellt oder Besucher gezählt. Wenn diese Option aktiviert war, wird empfohlen, eine Qualitätssicherung in älteren Browsern durchzuführen, um ein gutes Kundenerlebnis zu gewährleisten.

## „at.js“ herunterladen

Anweisungen zum Herunterladen der Bibliothek mithilfe der [!DNL Target] oder der Download-API.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) ist die bevorzugte Methode zum Implementieren von [!DNL Target] und der at.js-Bibliothek. Die folgenden Informationen sind bei Verwendung von Tags in [!DNL Adobe Experience Platform] zur Implementierung von [!DNL Target] nicht anwendbar.
>
>[!DNL Adobe Target] unterstützt sowohl at.js 1.*x* und in at.js 2.*x*. Aktualisieren Sie auf die neueste Version einer der Hauptversionen von at.js, um sicherzustellen, dass Sie eine unterstützte Version ausführen. Weitere Informationen zu den Funktionen in den einzelnen Versionen finden Sie unter [„at.js“-Versionsdetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Herunterladen von at.js über die [!DNL Target]

Herunterladen von at.js über die [!DNL Target]:

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.
1. Klicken Sie im Abschnitt Implementierungsmethoden auf die Schaltfläche **[!UICONTROL Download]** neben der gewünschten at.js-Version.

### Herunterladen von at.js mit der [!DNL Target] Download-API

So laden Sie at.js über die API herunter:

1. So finden Sie Ihren Clientcode.

   Der Client-Code ist oben auf der Seite **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** der [!DNL Target]-Benutzeroberfläche verfügbar.

1. So finden Sie Ihre Administratornummer.

   Laden Sie diese URL:

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   Ersetzen Sie `client code` durch den Clientcode aus Schritt 1.

   Das Ergebnis nach dem Laden dieser URL sollte in etwa wie im folgenden Beispiel aussehen:

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   In diesem Beispiel lautet die Administratornummer „6“.

1. at.js herunterladen.

   Laden Sie diese URL mit der folgenden Struktur. Durch Laden dieser URL wird der Download Ihrer benutzerdefinierten at.js-Datei gestartet.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * Ersetzen Sie `admin number` durch Ihre Administratornummer.
   * Ersetzen Sie `client code` durch den Clientcode aus Schritt 1.
   * Ersetzen Sie `version number` durch die gewünschte at.js-Versionsnummer (z. B. 2.2).

>[!WARNING]
>
>Das [!DNL Target]-Team verwaltet nur zwei Versionen von at.js - die aktuelle Version und die zweitneueste Version. Bitte aktualisieren Sie at.js nach Bedarf, um sicherzustellen, dass Sie eine unterstützte Version ausführen. Weitere Informationen zu den Funktionen in den einzelnen Versionen finden Sie unter [„at.js“-Versionsdetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

## at.js-Implementierung

at.js sollte im `<head>`-Element jeder Seite Ihrer Website implementiert werden.

Eine typische Implementierung von [!DNL Target], die keinen Tag-Manager verwendet, z. B. Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sieht wie folgt aus:

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

Beachten Sie folgende wichtige Hinweise:

* Verwenden Sie den Doctype HTML5 (z. B. `<!doctype html>`). Nicht unterstützte oder ältere Doctypes konnten dazu führen, dass [!DNL Target] keine Anfrage stellen konnten.
* Mit den Optionen zum Vorabladen und Vorabruf können Sie die Seitenladezeiten reduzieren. Wenn Sie diese Konfigurationen verwenden, stellen Sie sicher, dass Sie `<client code>` durch Ihren eigenen Client-Code ersetzen, den Sie auf der Seite **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** erhalten können.
* Wenn Sie über einen Daten-Layer verfügen, empfiehlt es sich, einen möglichst großen Teil im `<head>` Ihrer Seiten zu definieren, bevor „at.js“ geladen wird. Diese Platzierung bietet die maximale Möglichkeit, diese Informationen in [!DNL Target] für die Personalisierung zu verwenden.
* Spezielle [!DNL Target] wie `targetPageParams()`, `targetPageParamsAll()`, Datenanbieter und `targetGlobalSettings()` sollten nach dem Laden Ihrer Datenschicht und vor dem Laden von at.js definiert werden. Alternativ können diese Funktionen auch im Abschnitt Bibliothekskopfzeile der Seite at.js-Einstellungen bearbeiten gespeichert und als Teil der at.js-Bibliothek selbst gespeichert werden. Weitere Informationen zu diesen Funktionen finden Sie unter [at.js-Funktionen](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* Wenn Sie JavaScript-Hilfsbibliotheken wie jQuery verwenden, schließen Sie diese vor dem [!DNL Target] ein, damit Sie beim Erstellen [!DNL Target] Erlebnisse deren Syntax und Methoden verwenden können.
* Fügen Sie „at.js“ im `<head>` Ihrer Seiten hinzu.

## Konversionen verfolgen

Mit der Mbox für Auftragsbestätigungen werden Informationen zu Bestellungen auf Ihrer Seite gesammelt und die Berichterstellung basierend auf Umsatz und Aufträgen ermöglicht. Mit der Mbox für Auftragsbestätigungen können zudem Empfehlungsalgorithmen abgeleitet werden, beispielsweise „Personen, die x kauften, kauften auch y“.

>[!NOTE]
>
>Wenn Benutzer auf Ihrer Website Einkäufe tätigen, empfiehlt Adobe die Implementierung einer Mbox für Auftragsbestätigungen, auch wenn Sie Analytics for [!DNL Target] (A4T) für Ihr Reporting verwenden.

1. Fügen Sie auf Ihrer Bestellungsdetailseite das Mbox-Skript ein. Befolgen Sie dabei das folgende Modell:
1. Ersetzen Sie die WORTE IN GROSSBUCHSTABEN entweder durch dynamische oder statische Werte aus Ihrem Katalog.

   >[!TIP]
   >
   >Sie können Bestellungsinformationen auch in jeder Mbox übergeben (sie muss nicht `orderConfirmPage` benannt werden). Darüber hinaus können Bestellinformationen auch an mehrere Mboxes innerhalb derselben Kampagne weitergegeben werden.

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>Trennen Sie in der Mbox für Bestellbestätigungen mehrere Produkt-IDs durch Kommas.

Die Mbox für die Auftragsbestätigung verwendet die folgenden Parameter:

| Parameter | Beschreibung |
|--- |--- |
| orderId | Eindeutiger Wert zur Identifizierung einer Bestellung für die Konversionszählung.<p>Die `orderId` muss eindeutig sein. Doppelte Bestellungen werden in Berichten ignoriert. |
| orderTotal | Geldwert des Einkaufs.<p>Übergeben Sie den Wert ohne Währungssymbol. Verwenden Sie einen Dezimalpunkt (kein Komma), um die Dezimalwerte anzugeben. |
| productPurchasedId (optional) | Kommagetrennte Liste von Produkt-IDs, die innerhalb der Bestellung gekauft wurden.<p>Diese Produkt-IDs werden im Audit-Bericht angezeigt, um zusätzliche Berichtsanalysen zu unterstützen. |
