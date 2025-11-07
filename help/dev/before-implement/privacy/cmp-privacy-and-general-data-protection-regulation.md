---
keywords: DSGVO, EU, Europäische Union, Datenschutz, FAQ, Häufig gestellte Fragen, California Consumer Privacy Act, CCPA, Datenschutz, Datenschutz, Opt-out, Opt-out, Regierung, Regulierung, DSGVO5, DSGVO6, DSGVO7, DSGVO8, DSGVO9, EU0, EU1, EU2, EU3, EU4, EU5
description: Erfahren Sie mehr über Target und die Datenschutz-Grundverordnung (DSGVO) der Europäischen Union, den California Consumer Privacy Act (CCPA) und andere Datenschutzanforderungen.
title: Wie handhabt Target Datenschutzbestimmungen?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 62%

---

# Datenschutz und Datenschutzvorschriften

Hier erhalten Sie Informationen zur Datenschutz-Grundverordnung (DSGVO) der Europäischen Union, zum California Consumer Privacy Act (CCPA) und zu anderen Datenschutzbestimmungen. Erfahren Sie, wie sich diese Vorschriften auf Ihr Unternehmen und Adobe Target auswirken.

## Überblick über den Datenschutz und die Datenschutz-Grundverordnung (DSGVO) 

Am 25. Mai 2018 trat die DSGVO der Europäischen Union in Kraft. Weitere Informationen darüber, was diese Verordnung für Sie bedeutet, finden Sie unter [DSGVO und Ihr Unternehmen](https://business.adobe.com/de/privacy/general-data-protection-regulation.html).

Wenn Adobe einem Unternehmen Software und Dienstleistungen bereitstellt, tritt Adobe als Datenverarbeiter für alle personenbezogenen Daten auf, die im Rahmen dieser Dienstleistungen gespeichert und verarbeitet werden. Als Datenverarbeiter verarbeitet Adobe personenbezogene Daten gemäß den gewährten Berechtigungen und Anweisungen Ihres Unternehmens (z. B. über Angaben in Ihrer Vereinbarung mit Adobe).

Als Datenverantwortlicher legen Sie fest, welche personenbezogenen Daten Adobe in Ihrem Namen verarbeitet und speichert. Wenn Sie Adobe Experience Cloud-Lösungen nutzen, hostet Adobe abhängig von den verwendeten Lösungen und den Informationen, die Sie an Ihr Adobe Experience Cloud-Konto senden, möglicherweise personenbezogene Daten für Sie. Eine detaillierte Liste mit Beispielen finden Sie unter [Adobe Experience Cloud-Datenschutz](https://www.adobe.com/de/privacy/experience-cloud.html#collect).

Adobe Experience Cloud stellt Datenverantwortlichen DSGVO-konforme APIs bereit, mit denen sie die folgenden Aufgaben ausführen können:

* Auf die in Target gespeicherten Daten der betroffenen Person zugreifen
* Die in Target gespeicherten Daten der betroffenen Person löschen

Weitere Informationen finden Sie unter:

* [Übersicht über Adobe Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=de)
* [Privacy Service-API-Handbuch](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html?lang=de)
* Übersicht über die [Privacy Service-Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=de)

## Übersicht über den California Consumer Privacy Act (CCPA)

Der California Consumer Privacy Act (CCPA) bietet Verbrauchern in Kalifornien neue Rechte bezüglich ihrer personenbezogenen Daten und überträgt Unternehmen, die in Kalifornien Geschäfte treiben, Pflichten bezüglich des Datenschutzes. Der CCPA trat am 1. Januar 2020 in Kraft.

Das Gesetz überträgt den Bürgern Kaliforniens auf hoher Ebene verschiedene grundlegende Rechte, einschließlich folgender:

* Anforderung von Informationen (Datenzugriff)
* Abmeldung vom Verkauf personenbezogener Daten (ein weit gefasstes Recht zum Ausstieg aus der Freigabe von Informationen für Dritte)
* Löschen der personenbezogenen Daten
* Einholen von Informationen darüber, dass personenbezogene Daten bekannt gemacht oder verkauft werden

Wenn Sie sich im letzten Jahr auf das europäische Datenschutzrecht (DSGVO) vorbereitet haben, sind Ihnen einige dieser Rechte möglicherweise bekannt und viele der von Ihnen durchgeführten Aufgaben können umgewidmet werden.

>[!NOTE]
>
>Der Zugriff auf und das Löschen von Daten im Sinn des CCPA erfolgt auf dieselbe Weise wie für die DSGVO.

## Opt-in-Funktion in Adobe Target und Adobe Experience Platform

Target unterstützt die Opt-in-Funktionalität über Tags in Adobe Experience Platform und hilft Ihnen bei der Einwilligungsverwaltung. Mit der Opt-in-Funktion können Kunden steuern, wie und wann das Target-Tag ausgelöst wird. Es gibt auch eine Option über Adobe Experience Platform, um das Target-Tag vorab zu genehmigen. Um die Möglichkeit der Verwendung von Opt-in in der Target at.js-Bibliothek zu aktivieren, sollten Sie `targetGlobalSettings` verwenden und die `optinEnabled=true` hinzufügen. Wählen Sie in Adobe Experience Platform in der Dropdown-Liste DSGVO-Opt-in im Installationsfenster der Erweiterung „Aktivieren“ aus. Weitere [&#x200B; finden Sie unter „Implementieren von Target &#x200B;](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) Adobe Experience Platform&quot;.

Im folgenden Code-Snippet wird gezeigt, wie Sie die `optinEnabled=true`-Einstellung aktivieren:

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>Die Opt-in-Funktionalität wird in at.js-Version 1.7.0 und at.js 2.1.0 oder höher unterstützt. Die Opt-in-Funktion wird nicht in at.js-Version 2.0.0 und 2.0.1 unterstützt.

Opt-in-Verwaltung mit Adobe Experience Platform wird empfohlen. In Adobe Experience Platform können Sie präziser steuern, ob ausgewählte Seitenelemente vor der Target-Auslösung ausgeblendet werden sollen, was Ihnen bei der Einwilligungsverwaltung helfen kann.

In Verbindung mit dem Opt-in gibt es drei Szenarien:

1. **Das Target-Tag wird vorab über Adobe Experience Platform genehmigt (oder die betroffene Person hat zuvor über Target genehmigt):** Das Target-Tag wird nicht für die Einwilligung gespeichert und funktioniert wie erwartet.
1. **Das Target-Tag wird NICHT vorab genehmigt und `bodyHidingEnabled` ist FALSE:** Das Target-Tag wird erst ausgelöst, wenn die Einwilligung vom Kunden eingeholt wurde. Bevor die Einwilligung eingeholt wird, ist nur der Standardinhalt verfügbar. Nachdem die Einwilligung eingeholt wurde, wird Target aufgerufen und der personalisierte Inhalte wird der betroffenen Person (Besucher) zur Verfügung gestellt. Da vor der Einwilligung nur der Standardinhalt verfügbar ist, ist die richtige Strategie entscheidend, wie z. B. eine Splash-Seite, die Seitenteile mit personalisierten Inhalten überdeckt. So wird gewährleistet, dass das Erlebnis für die betroffene Person (Besucher) einheitlich bleibt.
1. **Das Target-Tag wird NICHT vorab genehmigt und `bodyHidingEnabled` ist TRUE:** Das Target-Tag wird erst ausgelöst, wenn die Einwilligung vom Kunden eingeholt wurde. Bevor die Einwilligung eingeholt wird, ist nur der Standardinhalt verfügbar. Da jedoch `bodyHidingEnabled` auf TRUE festgelegt ist, bestimmt `bodyHiddenStyle`, welcher Inhalt auf der Seite ausgeblendet wird, bis das Target-Tag ausgelöst wird (oder die betroffene Person den Opt-in ablehnt, woraufhin der Standardinhalt angezeigt wird). `bodyHiddenStyle` ist standardmäßig als `body { opacity:0;}` festgelegt, wodurch das HTML-Body-Tag ausblendet wird. Die empfohlene Seitenkonfiguration von Adobe finden Sie unten. So können Sie den gesamten Hauptteil der Seite – abgesehen vom Einwilligungsdialog – ausblenden, indem Sie den Seiteninhalt in einen und den Einwilligungsdialog in einen anderen Container einfügen. Mit diesem Setup wird Target so konfiguriert, dass nur der Container mit dem Seiteninhalt ausgeblendet wird. Siehe [Übersicht über Privacy Service](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=de&).

   Die empfohlene Seitenkonfiguration für Szenario 3 lautet wie folgt:

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   Davon ausgehend, dass `bodyHiddenStyle` folgenden Wert aufweist:

   ```
   #pageContent { opacity:0;}
   ```

## Häufig gestellte Fragen zu Datenschutz und Datenschutzvorschriften

Häufig gestellte Fragen zur Datenschutz-Grundverordnung (DSGVO) der Europäischen Union, zum California Consumer Privacy Act (CCPA) und anderen internationalen Datenschutzanforderungen für Target.

### Wie lautet die Adobe-Richtlinie für diese Vorschriften?

Adobe erfüllt seine Verpflichtungen als Datenverarbeiter bereits oder ist dabei, die entsprechenden Maßnahmen zu implementieren. Adobe verfügt durch Sicherheitszertifikate und integrierte Datenschutzoptionen über eine solide Basis, die durch zusätzliche Verbesserungen bis zum Stichtag im Mai 2018 weiter verstärkt wurden. Unternehmenskunden sind dafür verantwortlich, diese Verbesserungen zu implementieren sowie die erforderlichen Richtlinien und Vorgehensweisen zu aktualisieren.

### Muss mein Unternehmen als Datenverantwortlicher eine DSGVO- oder CCPA-Anfrage für jede verwendete Adobe Experience Cloud-Lösung einreichen?

Nein, Adobe bietet eine zentrale Möglichkeit, um Datenverantwortliche bei der Erfüllung von DSGVO- und CCPA-Anforderungen zu unterstützen. Datenverantwortliche müssen dazu nicht jede Lösung einzeln aufrufen.

Alle DSGVO- und CCPA-Anfragen in Experience Cloud-Lösungen, einschließlich Target, werden über eine zentrale Adobe-API vorgenommen, die zurzeit als DSGVO-API bezeichnet wird. Die API führt die Anfrage daraufhin in der gesamten Experience Cloud-Lösungs-Suite des Datenverantwortlichen aus.

### Für welche Informationen ermöglicht Adobe eine Löschung, wenn Kunden von betroffenen Personen oder Benutzern dazu aufgefordert werden?

In Target sind die Informationen zu den einzelnen Besuchern im jeweiligen Target-Besucherprofil enthalten. Target ermöglicht Kunden das Löschen aller Daten, die mit einer ID in ihrem Besucherprofil verbunden sind. Beispiele für die Profildatenspeicher in Target finden Sie unter [Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de).

Aggregierte oder anonymisierte Daten (beispielsweise Berichtsdaten), in denen keine Person identifiziert wird, oder Daten, die nicht mit einer bestimmten Person in Verbindung gebracht werden können (beispielsweise Inhaltsdaten), werden bei der Löschungsanfrage eines Benutzers nicht berücksichtigt.

Target-Besucherprofile, die seit 90 Tagen inaktiv sind, werden standardmäßig gelöscht, ohne dass eine weitere Aktion erforderlich ist.

### Welche IDs werden unterstützt, um Kunden zu helfen, eine DSGVO- oder CCPA-Zugriffs- und -Löschungsanfrage für Target durchzuführen?

Target unterstützt die folgenden ID-Typen zum Auffinden eines Kundenprofils:

| Benutzer-ID | Namespace-ID-Typ | Namespace-ID | Definition |
|--- |--- |--- |--- |
| Experience Cloud ID (ECID) | Standard | 4 | Adobe Experience Cloud ID, früher als Besucher-ID oder Experience Cloud ID bezeichnet. Sie können die JavaScript-API verwenden, um diese ID zu finden (siehe Details unten). |
| TnT-ID/Cookie-ID (TNTID) | Standard | 9 | Zielkennung, die als Cookie im Browser des Besuchers festgelegt wird. Sie können die JavaScript-API verwenden, um diese ID zu finden (siehe Details unten). |
| Drittanbieter-ID/CRM-ID (THIRDPARTYID) | Target-spezifisch | K. A. | Wenn Sie Target mit Ihrem CRM oder andere eindeutige Kennungsinformationen für Ihre Kunden bereitstellen. |

>[!NOTE]
>
>Obwohl Target Domain-übergreifende Cookies von Erstanbietern und Drittanbietern unterstützt, werden Erstanbieter-Target-Cookies nur für die DSGVO und CCPA empfohlen.

### Wie verwaltet Target Einverständnisse?

Die DSGVO und der CCPA schreiben nicht fest, wann Sie eine Einwilligung einholen müssen, sondern nur, wie Sie diese Einwilligung einholen. Die Einwilligungsstrategie jedes Kunden hängt von den erfassten Daten, den Verwendungspraktiken und den Datenschutzrichtlinien des Kunden ab. Die Einverständnisverwaltung wird von nicht unterstützt und sollte nicht über Target für die DSGVO und den CCPA erreicht werden.

Adobe bietet zurzeit keine Lösung zur Verwaltung von Einwilligungen. Auf dem Markt werden jedoch verschiedene Tools entwickelt, durch die einige der neuen Anforderungen abgedeckt werden. Weitere Informationen zu Datenschutztools im Allgemeinen, einschließlich Tools zur Einwilligungsverwaltung, finden Sie auf der Website der [International Association of Privacy Professionals (iapp)](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf) unter *2017 Privacy Tech Vendor Report*.

Target bietet Opt-in-Funktionalität über Adobe Experience Platform zur Unterstützung Ihrer Einwilligungsverwaltung. Mit der Opt-in-Funktion können Kunden steuern, wie und wann das Target-Tag ausgelöst wird. Es gibt auch eine Option über Adobe Experience Platform, um das Target-Tag vorab zu genehmigen. Opt-in-Verwaltung mit Adobe Experience Platform wird empfohlen. In Adobe Experience Platform gibt es eine präzisere Steuerung, um ausgewählte Seitenelemente vor der Target-Auslösung auszublenden, was Ihnen bei der Einwilligungsverwaltung helfen kann.

Weitere Informationen zur DSGVO, zum CCPA und zur Adobe Experience Platform finden Sie unter [Die Adobe Privacy JavaScript Library und die DSGVO](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=de&). Lesen Sie auch den obigen Abschnitt *Adobe Target- und Adobe Experience Platform-Opt-in*.

### Übermittelt `AdobePrivacy.js` Informationen an die DSGVO-API?

AdobePrivacy.js übermittelt *nicht* diese Informationen an die API. Dies muss der Kunde übernehmen. Die Bibliothek stellt nur die IDs bereit, die im Browser für einen bestimmten Besucher gespeichert wurden.

### Welche Daten werden von `removeIdentities` entfernt?

`removeIdentities` *entfernt nur* die IDs im Browser. Das gilt nur dann, wenn die Adobe-Lösung dies implementiert hat.

Target löscht beispielsweise die Cookies, in denen seine IDs gespeichert werden. Adobe Audience Manager (AAM) löscht jedoch nicht die demdex-ID, die in einem Drittanbieter-Cookie gespeichert ist.

### Welche Informationen müssen in einer Target-DSGVO- oder -CCPA-Anfrage enthalten sein?

Zusätzlich zu den Anforderungen der Central Privacy Service enthält eine gültige DSGVO- oder CCPA-Anfrage für Target folgende Elemente:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### Welche Arten von Antworten von Target über die DSGVO-API kann ich erwarten? 

| Anfragestatus | Target-Antwortnachricht | Szenario |
|--- |--- |--- |
| Verarbeitung läuft | Verarbeitung läuft | Target hat die DSGVO- oder CCPA-Anfrage erhalten und hat mit der Verarbeitung begonnen. |
| Abgeschlossen | Nicht zutreffend: Der Unternehmenskontext ist nicht zutreffend | Die IMS-ID in der DSGVO- oder CCPA-Anfrage ist keinem Target-Client zugeordnet.<br />Einige Unternehmen verfügen über mehrere IMS-IDs. Senden Sie die IMS-ID, in der Target bereitgestellt wurde. |
| Abgeschlossen | Nicht zutreffend: Benutzerkontext nicht gefunden | Die in der DSGVO- oder CCPA-Anfrage angegebene ID für den spezifischen Besucher oder die betroffene Person ist nicht im Target-Profilspeicher vorhanden.<br />Dieses Ergebnis wird auch zurückgegeben, wenn Sie versuchen, einen Namespace-ID-Typ zu übermitteln, der von Target nicht unterstützt wird (unterstützte IDs finden Sie oben). |
| Fehler | Fehlermeldung (abhängig vom Fehlertyp) | Fehler beim Abrufen oder Löschen des angeforderten Profils der betroffenen Person.<br />Fehler beim Hochladen in Azure für die Zugriffsanfrage. |

### Welche Antwort sendet Target bei einer Zugriffsanfrage an die DSGVO-API?

Antworten auf Anfragen nach Zugriff auf Daten enthalten eine Zusammenfassung des Target-Profils für den betroffenen Besucher. Diese Antwort wird an die Experience Cloud-DSGVO-API gesendet, die wiederum die Antwort an die Datenverantwortlichen weiterleitet.

Beispiel für eine Antwort der Target-API auf eine Zugriffsanfrage:

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| Feld | Beschreibung |
|--- |--- |
| jobId | Gibt die DSGVO- oder CCPA-Auftrags-ID aus der zentralen DSGVO-API an. |
| imsOrgID | Stellt eine eindeutige Kennung für Ihr Unternehmen bereit. |
| namespace | Wird auch als Datenquelle bezeichnet. Siehe „Welche IDs werden unterstützt, um Kunden zu helfen, Datenzugriffs- und Löschungsanfragen gemäß DSGVO oder CCPA in Target nachzukommen?“ in diesem Thema. |
| type | Der Typ der ID, für die Sie den Datenzugriff nach DSGVO oder CCPA angefordert haben. Target akzeptiert mehrere standardmäßige und Target-spezifische ID-Typen. Siehe „Welche IDs werden unterstützt, um Kunden zu helfen, Datenzugriffs- und Löschungsanfragen gemäß DSGVO oder CCPA in Target nachzukommen?“ in diesem Thema. |
| value | Die ID des Namespace/der Datenquelle. Siehe „Welche IDs werden unterstützt, um Kunden zu helfen, Datenzugriffs- und Löschungsanfragen gemäß DSGVO oder CCPA in Target nachzukommen?“ für gültige Werte. |
| integration code | Bei Integrationscode handelt es sich um Anzeigenamen für Ihre Datenquellen, die statt Datenquellen-IDs verwendet werden, um Ihnen den Überblick über Ihre Datenquellen zu erleichtern. |

Wenn mehrere Werte zur Bestimmung von Profilen angegeben werden, verfügt jede gültige ID über eine Profildatei. Eine oder mehrere Profildateien werden in Form einer JSON-Antwort des Zielprofils über die zentrale DSGVO-API an das zentrale DSGVO-Azure Blob gesendet.

Im Folgenden finden Sie ein Beispiel für eine Target-Profil-JSON:

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

Die im Beispiel verwendeten JSON-Felder des Profils werden in der folgenden Tabelle beschrieben:

| Feld | Beschreibung |
|--- |--- |
| Sample_Parameter | Viele Informationen im Target-Profil werden vom Datenverantwortlichen hochgeladen oder direkt bereitgestellt. In diesem Beispiel wurde ein Parameter im Target-Profil mithilfe der API zur Profilaktualisierung hochgeladen. Weitere Informationen finden Sie unter [Verfahren für die Datenübernahme in Target](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md). |
| user.ReturnTimeOfDay | Dieses Standardfeld enthält die Tageszeit des letzten wiederkehrenden Besuchs einer Benutzerin oder eines Benutzers. |
| firstSessionStart | Dieses Standardfeld enthält die Tageszeit, zu der die erste Sitzung des Benutzers begonnen hat. |
| user.sessionCountScript | Viele Informationen im Target-Profil werden vom Datenverantwortlichen hochgeladen oder direkt bereitgestellt. In diesem Beispiel erhöht ein Profilskript die Anzahl der Sitzungen, die dieser Besucher auf der Website des Datenverantwortlichen durchgeführt hat. Weitere Informationen finden Sie unter [Profilskript-Attribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=de). |

>[!NOTE]
>
>Dieses Code-Beispiel ist eine gekürzte Version einer JSON-Datei des Zielprofils. Bei zahlreichen Feldern im Target-Profil handelt es sich nicht um Standardfelder. Die zurückgegebenen Daten hängen von den Informationen im jeweiligen Besucherprofil ab.

### Unterstützt Target IP-Verschleierung? 

Target unterstützt die IP-Verschleierung, wenn Sie sie im Rahmen Ihrer DSGVO- oder CCPA-Implementierungsstrategie verwenden. Weitere Informationen finden Sie unter [Datenschutz](privacy.md#replacement-of-last-octet-of-ip-addresses).

### Sollte ich etwas unternehmen, um zu verhindern, dass meine Daten an Dritte weitergegeben oder verkauft werden?

Target ermöglicht es Kunden nicht, Daten direkt über Target an Dritte weiterzugeben oder zu verkaufen, weshalb es für Target keine Opt-out-Option für den Verkauf gibt.
