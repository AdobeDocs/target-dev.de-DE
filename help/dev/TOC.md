---
user-guide-title: Adobe Target-Entwicklerhandbuch
breadcrumb-title: Target-Entwicklerhandbuch
user-guide-description: Erfahren Sie, wie Sie das Kundenerlebnis so anpassen und personalisieren können, dass Sie den Umsatz Ihrer Websites, Mobile Sites, Mobile Apps, Social Media und anderer digitaler Kanäle maximieren können.
source-git-commit: c963a070a7a4c5e7dc2915eb5ac7d60895340705
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 45%

---


# Adobe Target-Entwicklerhandbuch {#developer}

+ [Adobe Target-Entwicklerhandbuch](overview.md)
+ Erste Schritte {#implementation}
   + Vor der Implementierung {#before-implement}
      + [Vor der Implementierung](before-implement/considerations-before-you-implement-target.md)
      + [Vorbereiten der Target-Implementierung](before-implement/prepare-to-implement-target.md)
   + Datenschutz und Sicherheit {#privacy}
      + [Datenschutz – Überblick](before-implement/privacy/privacy.md)
      + [Vorschriften zur Privatsphäre und zum Datenschutz](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Cookies in Target](before-implement/privacy/cookie-behavior.md)
      + [Löschen des Target-Cookies](before-implement/privacy/cookie-deleting.md)
      + [Auswirkungen der Einstellung von Drittanbieter-Cookies auf Target (at.js)](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [SameSite-Cookie-Richtlinien von Google Chrome](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Apple Intelligent Tracking Prevention (ITP) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [Richtlinien zur Content Security Policy (CSP)](before-implement/privacy/content-security-policy.md)
      + [Zulassungsliste für Target-Edge-Knoten](before-implement/privacy/allowlist-edges.md)
   + Verfahren für die Datenübernahme in Target {#methods}
      + [Methodenübersicht](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [Seitenparameter](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [In-Page-Profilattribute](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [Skriptprofilattribute](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [Datenanbieter](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [API zur Massenaktualisierung von Profilen](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [API zur Aktualisierung einzelner Profile](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [Kundenattribute](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [Profil-API-Einstellungen](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Target-Sicherheitsübersicht](before-implement/target-security-overview.md)
   + [Unterstützte Browser](before-implement/supported-browsers.md)
   + [Änderungen der TLS-Verschlüsselung (Transport Layer Security)](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME und Adobe Target](before-implement/implement-cname-support-in-target.md)
+ Client-seitige {#client-side}
   + [Übersicht: Target für Client-seitiges Web implementieren](implement/client-side/overview.md)
   + [Übersicht über die Implementierung von Adobe Experience Platform Web SDK](implement/client-side/aep-web-sdk.md)
   + at.js-Implementierung {#at-js-implementation}
      + [Übersicht über at.js](implement/client-side/atjs/how-atjs-works/overview.md)
      + Funktionsweise von „at.js“ {#at-js}
         + [Funktionsweise von at.js – Überblick](implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [Verwaltung von Flackern mit „at.js“](implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [„at.js“-Integrationen](implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + Bereitstellen von „at.js“ {#deploy-at-js}
         + [Bereitstellen von „at.js“](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [Implementierung von Target mithilfe von Adobe Experience Platform](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [Implementieren von Target ohne einen Tag-Manager](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [Implementieren von Target mit dem dynamischen Tag-Manager (DTM)](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [Implementieren von Target für Einzelseitenanwendungen (SPA)](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + Geräteinterne Entscheidungsfindung {#on-device-decisioning}
         + [Übersicht über On-device Decisioning](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [Unterstützte Funktionen](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [Regelartefakt](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [Fehlerbehebung](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + „at.js“-Funktionen {#functions-overview}
         + [„at.js“-Funktionen – Überblick](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine() und mboxUpdate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension() - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [Benutzerdefinierte at.js-Ereignisse](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [„at.js“-Debugging mit dem Adobe Experience Cloud-Debugger](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [Verwenden Cloud-basierter Instanzen mit Target](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [Häufig gestellte Fragen zu „at.js“](implement/client-side/atjs/target-atjs-faq.md)
      + [„at.js“-Versionsdetails](implement/client-side/atjs/target-atjs-versions.md)
      + [Aktualisieren von at.js 1.x auf at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [„at.js“-Cookies](implement/client-side/atjs/atjs-cookies.md)
   + [User-agent und Client Hints](implement/client-side/atjs/user-agent-and-client-hints.md)
   + Erläuterung der globalen Mbox {#global-mbox}
      + [Globale Mbox – Überblick](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [Anpassen einer globalen Mbox](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [Verwenden einer globalen Mbox in einer Legacy-Implementierung](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [Übergeben von Parametern an eine globale Mbox](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [Häufig gestellte Fragen zu globalen Mboxes](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ Server-seitige {#server-side}
   + [Serverseitig: Target-Implementierung – Überblick](implement/server-side/server-side-overview.md)
   + [Erste Schritte mit Target-SDKs](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [Beispiel-Apps](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [Übergang von Target-Legacy-APIs zu Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + Grundprinzipien {#core-principles}
      + [Übersicht über die Grundprinzipien](implement/server-side/sdk-guides/core-principles/overview.md)
      + [Benutzer-ID und Bucketing](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [Zielgruppen-Targeting](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [Ereignis-Tracking](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [Benutzerberechtigungen und Eigenschaften](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + {#integration}
      + [Übersicht über die Integration](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Experience Cloud-ID-Dienst (ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Berichterstellung von Analytics for Target (A4T)](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [AAM-Segmente](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + {#on-device-decisioning} der geräteinternen Entscheidungsfindung
      + [Übersicht über On-device Decisioning](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + {#rule-artifact} von Regelartefakten
         + [Übersicht über Regelartefakte](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [Herunterladen über Adobe Target SDK](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [Über JSON-Payload herunterladen](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [Beispiel für ein Regelartefakt](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [Ausführen von A/B-Tests mit Feature Flags](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [Ausführen von Funktionstests mit Attributen](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [Verwalten von Rollouts für Funktionstests](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [Personalisierung bereitstellen](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [Übersicht über die unterstützten Funktionen](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [Fehlerbehebung bei der geräteinternen Entscheidungsfindung](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [Best Practices  ](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Node.js SDK-{#node-js}
      + [Übersicht über Node.js SDK](implement/server-side/node-js/overview.md)
      + [Installieren der Node.js-SDK](implement/server-side/node-js/install-sdk.md)
      + [Initialisieren der Node.js-SDK](implement/server-side/node-js/initialize-sdk.md)
      + [Abrufen von Angeboten (Node.js)](implement/server-side/node-js/get-offers.md)
      + [Abrufen von Attributen (Node.js)](implement/server-side/node-js/get-attributes.md)
      + [Senden von Benachrichtigungen (Node.js)](implement/server-side/node-js/send-notifications.md)
      + [SDK-Ereignisse (Node.js)](implement/server-side/node-js/sdk-events.md)
      + [Logger (Node.js)](implement/server-side/node-js/logger.md)
      + [Proxy-Konfiguration (Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Java SDK-{#java}
      + [Übersicht über Java SDK](implement/server-side/java/overview.md)
      + [Installieren der Java-SDK](implement/server-side/java/install-sdk.md)
      + [Initialisieren der Java-SDK](implement/server-side/java/initialize-sdk.md)
      + [Angebote abrufen (Java)](implement/server-side/java/get-offers.md)
      + [Abrufen von Attributen (Java)](implement/server-side/java/get-attributes.md)
      + [Benachrichtigungen senden (Java)](implement/server-side/java/send-notifications.md)
      + [SDK-Ereignisse (Java)](implement/server-side/java/sdk-events.md)
      + [Logger (Java)](implement/server-side/java/logger.md)
      + [Asynchrone Anforderungen (Java)](implement/server-side/java/asynchronous-requests.md)
      + [Proxy-Konfiguration (Java)](implement/server-side/java/proxy-configuration.md)
      + [Benutzerdefinierte HTTP-Client-Konfiguration (Java)](implement/server-side/java/custom-http-client.md)
      + [Dienstprogrammmethoden (Java)](implement/server-side/java/utility-methods.md)
   + .NET SDK-{#net}
      + [Übersicht über .NET SDK](implement/server-side/net/overview.md)
      + [Installieren von .NET SDK](implement/server-side/net/install-sdk.md)
      + [Initialisieren von .NET SDK](implement/server-side/net/initialize-sdk.md)
      + [Angebote abrufen (.NET)](implement/server-side/net/get-offers.md)
      + [Abrufen von Attributen (.NET)](implement/server-side/net/get-attributes.md)
      + [Benachrichtigungen senden (.NET)](implement/server-side/net/send-notifications.md)
      + [SDK-Ereignisse (.NET)](implement/server-side/net/sdk-events.md)
      + [Asynchrone Anforderungen (.NET)](implement/server-side/net/asynchronous-requests.md)
   + Python SDK-{#python}
      + [Übersicht über Python SDK](implement/server-side/python/overview.md)
      + [Installieren von Python SDK](implement/server-side/python/install-sdk.md)
      + [Initialisieren von Python SDK](implement/server-side/python/initialize-sdk.md)
      + [Abrufen von Angeboten (Python)](implement/server-side/python/get-offers.md)
      + [Attribute abrufen (Python)](implement/server-side/python/get-attributes.md)
      + [Benachrichtigungen senden (Python)](implement/server-side/python/send-notifications.md)
      + [SDK-Ereignisse (Python)](implement/server-side/python/sdk-events.md)
      + [Asynchrone Anfragen (Python)](implement/server-side/python/asynchronous-requests.md)
      + [Logger (Python)](implement/server-side/python/logger.md)
+ [Hybridimplementierung](implement/hybrid/hybrid-overview.md)
+ [Recommendations-Implementierung](implement/recommendations/recommendations.md)
+ [Recommendations-Implementierung - Beta](/help/dev/implement/recommendations/recommendations-beta.md)
+ {#mobile-apps} der Mobile-App-Implementierung
   + [Target für mobile Apps – Überblick](implement/mobile/overview.md)
   + [Mobile Target-Vorschau](implement/mobile/target-mobile-preview.md)
   + [Verwenden des Standortdienstes](implement/mobile/use-location-service.md)
   + [Target für mobile Apps – FAQs](implement/mobile/mobile-faq.md)
   + [Implementieren von Target mit dem AEP Mobile SDK in einer nativen App mit Web-Ansichten](/help/dev/implement/mobile/native-app.md)
+ E-Mail-{#implement-email}
   + [E-Mail: Target-Implementierung – Überblick](implement/email/overview.md)
   + [Erstellen einer AdBox für ein Bild](implement/email/testing-content-with-the-adbox.md)
   + [Testen einer E-Mail-Bild-AdBox](implement/email/testing-email-image-adbox.md)
   + [Arbeiten mit Weiterleitungen](implement/email/working-with-redirectors.md)
+ API-Handbücher {#api}
   + [Target-API - Übersicht](/help/dev/before-administer/target-api-overview.md)
   + [Konfigurieren der Authentifizierung für Target-APIs](/help/dev/before-administer/configure-authentication.md)
   + Handbuch zur Bereitstellungs-API {#delivery-api}
      + [Übersicht über die Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md)
      + [SDKs für die Interaktion mit der Bereitstellungs-API](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [Erste Schritte](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [Benutzerberechtigungen (Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [Identifizieren von Besuchern](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [Einzel- oder Batch-Versand](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [Vorabruf](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [Benachrichtigungen](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [Integration mit Experience Cloud](before-implement/delivery-api-overview/integration.md)
      + [Überlegungen und bekannte Einschränkungen](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [Client-Hinweise](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [Bereitstellungs-API](/help/dev/implement/delivery-api/delivery-api.md)
   + Admin-API-{#admin-api}
      + [Übersicht über die Admin-API](before-administer/admin-api-overview/admin-api-overview.md)
      + [Adobe Target Admin-API](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + Profil-API-{#profile-apis}
      + [Profile-API - Übersicht](/help/dev/administer/profile-api/profiles-api.md)
      + [Profile abrufen](/help/dev/administer/profile-api/profile-fetch.md)
      + [Profilaktualisierung](/help/dev/administer/profile-api/profile-api-overview.md)
      + [API zur Aktualisierung einzelner Profile](/help/dev/administer/profile-api/profile-single-api.md)
      + [API zur Massenaktualisierung von Profilen](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [Berichterstellungs-API](/help/dev/administer/reporting-api/reporting-api.md)
   + Recommendations API-{#recommendations-api}
      + [Übersicht über die Recommendations-API](before-administer/recs-api/overview.md)
      + [Katalog mit APIs verwalten](before-administer/recs-api/manage-catalog.md)
      + [Verwalten benutzerdefinierter Kriterien](before-administer/recs-api/manage-custom-criteria.md)
      + [Verwenden der Bereitstellungs-API mit Recommendations](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [Recommendations-API](/help/dev/administer/recommendations-api/recommendations-api.md)
   + Models-API-{#models-api}
      + [Auf die Blockierungsliste setzen Übersicht über die Models-API](before-administer/models-api.md)
      + [Models-API](/help/dev/administer/models-api/models-api-overview.md)
   + [Adobe Admin Console-APIs](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [Adobe Experience Platform Edge Network Server-API](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ Implementierungsmuster {#implementation-patterns}
   + [Übersicht über Implementierungsmuster](/help/dev/patterns/pattern-overview.md)
   + Recommendations-Implementierungsmuster unter Verwendung von at.js-{#atjs}
      + [Recommendations-Implementierungsmuster mit at.js - Übersicht](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [SDKs initialisieren](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [Konfigurieren der Datenerfassung](/help/dev/patterns/recs-atjs/data-collection.md)
      + [Rendern von Erlebnissen](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [Zielgruppe benachrichtigen](/help/dev/patterns/recs-atjs/notify-target.md)


