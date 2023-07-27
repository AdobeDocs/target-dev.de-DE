---
keywords: Target implementieren, Implementierung, at.js implementieren, Tag-Manager, On-Device Decisioning, bei Geräteentscheidungen
description: Erfahren Sie, wie Sie die Einstellungen festlegen (Kontodetails, Implementierungsmethoden usw.). zur Implementierung der [!DNL Adobe Target] "at.js"-Bibliothek ohne Verwendung eines Tag-Managers.
title: Kann ich implementieren? [!DNL Target] ohne Tag-Manager?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 45%

---

# Implementierung [!DNL Target] ohne Tag-Manager

Informationen zur Implementierung [!DNL Adobe Target] ohne Verwendung von Tag-Manager oder -Tags in [!DNL Adobe Experience Platform].

>[!NOTE]
>
>Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) die bevorzugte Methode zur Implementierung von [!DNL Target] und der at.js-Bibliothek. Die folgenden Informationen gelten nicht für die Verwendung von Tags in [!DNL Adobe Experience Platform] zur Implementierung [!DNL Target].

Klicken Sie auf die Schaltfläche , um auf die Seite Implementierung zuzugreifen. **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.

Sie können die folgenden Einstellungen auf dieser Seite angeben:

* Kontodetails
* Implementierungsmethoden
* Profil-API
* Debugger-Tools
* Datenschutz

>[!NOTE]
>
>Sie können Einstellungen in der at.js-Bibliothek überschreiben, anstatt sie in der [!DNL Target] Standard/Premium-Benutzeroberfläche oder durch Verwendung von REST-APIs. Weitere Informationen finden Sie unter [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## Kontodetails

Sie können die folgenden Kontodetails anzeigen. Diese Einstellungen können nicht geändert werden.

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Clientcode] | Der Clientcode ist eine clientspezifische Folge von Zeichen, die oft benötigt wird, wenn die [!DNL Target]-APIs zum Einsatz kommen. |
| [!UICONTROL IMS-Organisations-ID] | Diese ID ordnet die Implementierung Ihrem Adobe Experience Cloud-Konto zu. |
| [!UICONTROL On-Device Decisioning] | Um die Entscheidungsfindung auf dem Gerät zu aktivieren, schieben Sie den Umschalter in die Position &quot;Ein&quot;.<p>Mit der Entscheidungsfindung auf dem Gerät können Sie Ihre A/B- und Erlebnis-Targeting-Kampagnen (XT) auf Ihrem Server zwischenspeichern und speicherinterne Entscheidungen bei nahezu null Latenz treffen. Weitere Informationen finden Sie unter [Einführung in die geräteübergreifende Entscheidungsfindung](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL Alle vorhandenen Entscheidungsaktivitäten auf dem Gerät in das Artefakt einschließen] | (Bedingt) Diese Option wird angezeigt, wenn Sie die Entscheidungsfindung auf dem Gerät aktivieren.<p>Schieben Sie den Umschalter in die &quot;Ein&quot;-Position, wenn Sie alle Ihre Live-Nachrichten [!DNL Target] Aktivitäten, die für die Entscheidungsfindung auf dem Gerät qualifiziert sind, automatisch in das Artefakt aufgenommen werden.<p>Wenn Sie diesen Umschalter deaktivieren, müssen Sie alle Entscheidungsaktivitäten auf dem Gerät neu erstellen und aktivieren, damit sie in das generierte Regelartefakt aufgenommen werden. |

## Implementierungsmethoden

Die folgenden Einstellungen können im Bereich Implementierungsmethoden konfiguriert werden:

### Globale Einstellungen

>[!NOTE]
>
>Diese Einstellungen werden auf alle [!DNL Target] .js-Bibliotheken. Nachdem Sie Änderungen im Abschnitt &quot;Implementierungsmethoden&quot;vorgenommen haben, müssen Sie die Bibliothek herunterladen und in Ihrer Implementierung aktualisieren.

| Einstellung | Beschreibung |
| --- | --- |
| [!UICONTROL Seitenladung aktiviert (globale Mbox automatisch erstellen)] | Wählen Sie aus, ob der globale Mbox-Aufruf in die Datei at.js integriert werden soll, damit er automatisch bei jedem Laden der Seite aktiviert wird. |
| [!UICONTROL Globale mbox] | Wählen Sie einen Namen für die globale Mbox aus. Der Standardname lautet target-global-mbox.<p>Sonderzeichen wie das kaufmännische Und (&amp;) können mit at.js für Mbox-Namen verwendet werden. |
| [!UICONTROL Zeitüberschreitung (Sekunden)] | Falls [!DNL Target] nicht innerhalb des festgelegten Zeitraums mit Inhalten antwortet, erfolgt ein Timeout für den Server-Aufruf und es werden Standardinhalte angezeigt. Während der Sitzung des Besuchers werden weiter Aufrufe durchgeführt. Der Standardwert liegt bei 5 Sekunden.<p>Die Bibliothek at.js verwendet die Timeout-Einstellung in `XMLHttpRequest`. Der Timeout beginnt, wenn die Anforderung ausgelöst wird, und endet, wenn [!DNL Target] eine Antwort von dem Server erhält. Weitere Informationen dazu finden Sie unter [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout) im Mozilla Developer Network.<p>Tritt der festgelegte Timeout vor Erhalt der Antwort ein, wird dem Besucher ein Standardinhalt angezeigt, und der Besucher wird möglicherweise als Teilnehmer in einer Aktivität gezählt, da die gesamte Datenerfassung am [!DNL Target]-Edge erfolgt. Erreicht die Anforderung den [!DNL Target]-Edge, wird der Besucher gezählt.<p>Beim Konfigurieren der Timeout-Einstellung müssen Sie Folgendes beachten:<ul><li>Wenn der Wert zu niedrig ist, erhalten Besucher wahrscheinlich meist nur den Standardinhalt angezeigt, auch wenn sie möglicherweise als Teilnehmer in einer Aktivität gezählt werden.</li><li>Ist der Wert zu hoch, werden Besuchern unter Umständen leere Stellen auf Ihrer Webseite oder komplett leere Seiten angezeigt, falls Sie für längere Zeiträume Textausblendung einsetzen.</li></ul>Genaueres über Mbox-Antwortzeiten erfahren Sie auf der Registerkarte „Netzwerk“ in den Entwicklertools Ihres Browsers. Sie können auch Tools zur Überwachung der Webleistung einsetzen, die von Drittanbietern stammen, wie zum Beispiel Catchpoint.<p>**Hinweis:** Die Einstellung [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) stellt sicher, dass [!DNL Target] nicht zu lange auf die Antwort der Besucher-API wartet. Diese Einstellung und die hier beschriebene Timeout-Einstellung für at.js beeinflussen sich nicht gegenseitig. |
| [!UICONTROL Profillebensdauer] | Mit dieser Einstellung legen Sie fest, wie lange Besucherprofile gespeichert werden. Profile werden standardmäßig zwei Wochen lang gespeichert. Diese Einstellung kann auf 90 Tage erhöht werden.<p>Wenden Sie sich an den [Kundendienst](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C), wenn Sie die Profillebensdauer ändern möchten. |

### Wichtigste Implementierungsmethode

>[!NOTE]
>
>[!DNL Adobe Target]  unterstützt beide at.js 1.*x* und at.js 2.*x*. Führen Sie ein Upgrade auf die neueste Aktualisierung der beiden Hauptversionen von at.js durch, um sicherzustellen, dass Sie eine unterstützte Version ausführen.

Um die gewünschte at.js-Version herunterzuladen, klicken Sie auf die entsprechende **Herunterladen** Schaltfläche.

Klicken Sie zum Bearbeiten der at.js-Einstellung auf **[!UICONTROL Bearbeiten]** neben der gewünschten at.js-Version.

>[!WARNING]
>
>Wenden Sie sich vor dem Ändern dieser Standardeinstellungen an die [Kundenunterstützung](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C) sodass Sie sich nicht auf Ihre aktuelle Implementierung auswirken.

Zusätzlich zu den oben erläuterten Einstellungen sind auch die folgenden spezifischen at.js-Einstellungen verfügbar:

| Einstellung | Beschreibung |
|--- |--- |
| Domänenübergreifend | Für at.js v1.*x*, geben Sie an, ob domänenübergreifende Funktionen `disabled` (Browser setzen Cookies nur in Ihrer Domäne (Erstanbieter-Cookies), `x only` (Browser setzen Cookies nur in der Target-Domäne) oder beide durch Auswahl von `enabled` (Browser setzen sowohl Erst- als auch Drittanbieter-Cookies.) Geben Sie für at.js v2.10 und höher an, ob domänenübergreifende Funktionen `enabled` (Browser setzen sowohl Erst- als auch Drittanbieter-Cookies) oder `disabled` (Browser setzen keine Drittanbieter-Cookies ein). |
| Benutzerdefinierte Bibliothekskopfzeile | Fügen Sie benutzerdefiniertes JavaScript hinzu, das oben in der Bibliothek aufgeführt wird. |
| Benutzerdefinierte Bibliotheksfußzeile | Fügen Sie benutzerdefiniertes JavaScript hinzu, das unten in der Bibliothek aufgeführt wird. |

### Profil-API

Aktivieren oder deaktivieren Sie die Authentifizierung für Batch-Aktualisierungen via API und generieren Sie ein Token für die Profilauthentifizierung.

Weitere Informationen finden Sie unter [Profil-API-Einstellungen](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### Debugger-Tools

Autorisierungstoken zur Verwendung erweiterter [!DNL Target] Debugging-Tools. Klicks **[!UICONTROL Neues Authentifizierungstoken generieren]**.

![Neues Authentifizierungstoken erstellen](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### Datenschutz

Mit diesen Einstellungen können Sie [!DNL Target] in Übereinstimmung mit den geltenden Datenschutzgesetzen.

Wählen Sie die gewünschte Einstellung aus der Dropdownliste Besucher-IP-Adresse verschleiern aus:

* Verschleierung des letzten Oktetts
* Gesamte IP-Verschleierung
* Keine

Weitere Informationen finden Sie unter [Datenschutz](/help/dev/before-implement/privacy/privacy.md).

>[!NOTE]
>
>Die Option Unterstützung älterer Browser war in at.js , Version 0.9.3 und älter verfügbar. Diese Option wurde in at.js, Version 0.9.4, entfernt. Eine Liste der von at.js unterstützten Browser finden Sie unter [Unterstützte Browser](/help/dev/before-implement/supported-browsers.md).<p>Bei älteren Browsern handelt es sich in der Regel um alte Versionen, die CORS (Cross Origin Resource Sharing) nicht vollständig unterstützen. Solche Browser sind zum Beispiel alle Versionen von Internet Explorer vor Version 11 oder Safari Version 6 und ältere Versionen. Wenn die Unterstützung älterer Browser deaktiviert war, [!DNL Target] keine Inhalte bereitgestellt hat oder Besucher in Berichten zu diesen Browsern gezählt hat. Wenn diese Option aktiviert wurde, wird empfohlen, eine Qualitätssicherung für ältere Browser durchzuführen, um ein gutes Kundenerlebnis zu gewährleisten.

## „at.js“ herunterladen 

Anleitung zum Herunterladen der Bibliothek mit dem [!DNL Target] -Benutzeroberfläche oder der Download-API.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) ist die bevorzugte Methode zur Implementierung von [!DNL Target] und der at.js-Bibliothek. Die folgenden Informationen gelten nicht für die Verwendung von Tags in [!DNL Adobe Experience Platform] zur Implementierung [!DNL Target].
>
>[!DNL Adobe Target] unterstützt beide at.js 1.*x* und at.js 2.*x*. Führen Sie ein Upgrade auf die neueste Aktualisierung einer der beiden Hauptversionen von at.js durch, um sicherzustellen, dass Sie eine unterstützte Version ausführen. Weitere Informationen zu den Funktionen in den einzelnen Versionen finden Sie unter [„at.js“-Versionsdetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

### Herunterladen von at.js mithilfe der [!DNL Target] Benutzeroberfläche

So laden Sie &quot;at.js&quot;aus dem [!DNL Target] -Schnittstelle:

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.
1. Klicken Sie im Abschnitt Implementierungsmethoden auf das **[!UICONTROL Herunterladen]** neben der gewünschten at.js-Version.

### Herunterladen von at.js mithilfe der [!DNL Target] Download-API

So laden Sie at.js mithilfe der API herunter.

1. So finden Sie Ihren Clientcode.

   Ihr Client-Code ist oben im **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** der [!DNL Target] -Schnittstelle.

1. So finden Sie Ihre Administratornummer.

   Laden Sie diese URL:

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   Ersetzen `client code` mit dem Clientcode aus Schritt 1.

   Das Ergebnis nach dem Laden dieser URL sollte in etwa wie im folgenden Beispiel aussehen:

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   In diesem Beispiel lautet die Administratornummer „6“.

1. Herunterladen von „at.js“. 

   Laden Sie diese URL mit der folgenden Struktur. Wenn Sie diese URL laden, wird der Download Ihrer angepassten at.js-Datei initiiert.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * Ersetzen `admin number` mit Ihrer Administratornummer.
   * Ersetzen `client code` mit dem Clientcode aus Schritt 1.
   * Ersetzen `version number` mit der gewünschten at.js-Versionsnummer (z. B. 2.2).

>[!WARNING]
>
>Die [!DNL Target] -Team verwaltet nur zwei Versionen von at.js - die aktuelle Version und die zweitneueste Version. Führen Sie bei Bedarf ein Upgrade von at.js durch, um sicherzustellen, dass Sie eine unterstützte Version ausführen. Weitere Informationen zu den Funktionen in den einzelnen Versionen finden Sie unter [„at.js“-Versionsdetails](/help/dev/implement/client-side/atjs/target-atjs-versions.md).

## at.js-Implementierung

at.js sollte im `<head>`-Element jeder Seite Ihrer Website implementiert werden.

Eine typische Implementierung von [!DNL Target] Verwendung eines Tag-Managers, z. B. Tags in [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) sieht wie folgt aus:

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

* Der Doctype HTML5 (z. B. `<!doctype html>`) verwendet werden. Nicht unterstützte oder ältere Dokumenttypen können zu [!DNL Target] keine Anfrage stellen können.
* Mit den Optionen zum Vorabladen und Vorabruf können Sie die Seitenladezeiten reduzieren. Wenn Sie diese Konfigurationen verwenden, stellen Sie sicher, dass Sie `<client code>` mit Ihrem eigenen Clientcode, den Sie aus dem **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** Seite.
* Wenn Sie über einen Daten-Layer verfügen, empfiehlt es sich, einen möglichst großen Teil im `<head>` Ihrer Seiten zu definieren, bevor „at.js“ geladen wird. Diese Platzierung bietet die maximale Möglichkeit, diese Informationen in [!DNL Target] zur Personalisierung.
* Sonderaktion [!DNL Target] Funktionen wie `targetPageParams()`, `targetPageParamsAll()`, Datenanbietern und `targetGlobalSettings()` sollte definiert werden, nachdem Ihre Datenschicht und bevor at.js geladen wird. Alternativ können diese Funktionen im Abschnitt &quot;Bibliothekskopfzeile&quot;der Seite &quot;at.js-Einstellungen bearbeiten&quot;gespeichert und als Teil der at.js-Bibliothek selbst gespeichert werden. Weitere Informationen zu diesen Funktionen finden Sie unter  [„at.js“-Funktionen](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* Wenn Sie JavaScript-Hilfsbibliotheken wie jQuery verwenden, schließen Sie sie vor ein [!DNL Target] verwenden, damit Sie beim Erstellen von [!DNL Target] Erlebnisse.
* Fügen Sie „at.js“ im `<head>` Ihrer Seiten hinzu.

## Konversionen verfolgen

Mit der Mbox für Auftragsbestätigungen werden Informationen zu Bestellungen auf Ihrer Seite gesammelt und die Berichterstellung basierend auf Umsatz und Aufträgen ermöglicht. Mit der Mbox für Auftragsbestätigungen können zudem Empfehlungsalgorithmen abgeleitet werden, beispielsweise „Personen, die x kauften, kauften auch y“.

>[!NOTE]
>
>Wenn Benutzer auf Ihrer Website Einkäufe tätigen, empfiehlt Adobe die Implementierung einer Mbox für Auftragsbestätigungen, auch wenn Sie Analytics für [!DNL Target] (A4T) für Ihre Berichterstellung.

1. Fügen Sie auf Ihrer Bestellungsdetailseite das Mbox-Skript ein. Befolgen Sie dabei das folgende Modell:
1. Ersetzen Sie die WORTE IN GROSSBUCHSTABEN entweder durch dynamische oder statische Werte aus Ihrem Katalog.

   >[!TIP]
   >
   >Sie können Bestellinformationen auch an beliebige Mboxes weitergeben (sie müssen nicht benannt werden). `orderConfirmPage`). Darüber hinaus können Bestellinformationen auch an mehrere Mboxes innerhalb derselben Kampagne weitergegeben werden.

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
>Trennen Sie mehrere Produkt-IDs in der Mbox für Auftragsbestätigungen durch Kommas.

Die Mbox für die Auftragsbestätigung verwendet die folgenden Parameter:

| Parameter | Beschreibung |
|--- |--- |
| orderId | Eindeutiger Wert zur Identifizierung einer Bestellung für die Konversionszählung.<p>`orderId` muss eindeutig sein. Doppelte Bestellungen werden in Berichten ignoriert. |
| orderTotal | Geldwert des Einkaufs.<p>Das Währungssymbol wird nicht übergeben. Verwenden Sie einen Dezimalpunkt (kein Komma), um die Dezimalwerte anzugeben. |
| productPurchasedId (optional) | Kommagetrennte Liste von Produkt-IDs, die innerhalb der Bestellung gekauft wurden.<p>Diese Produkt-IDs werden im Audit-Bericht angezeigt, um die zusätzliche Berichtanalyse zu unterstützen. |
