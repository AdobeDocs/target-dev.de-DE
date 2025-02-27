---
title: Abrufen von Recommendations mit der Bereitstellungs-API
description: Dieser Artikel führt Entwicklerinnen und Entwickler durch die Schritte, die zum Abrufen von Recommendations-Inhalten mithilfe der Adobe Target-Bereitstellungs-API erforderlich sind.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 1%

---

# Abrufen von Recommendations mit der Bereitstellungs-API

Die Recommendations-APIs von Adobe Target und Adobe Target können für die Bereitstellung von Antworten auf Web-Seiten verwendet werden. Sie können aber auch für Erlebnisse außerhalb von HTML verwendet werden, wie Apps, Bildschirme, Konsolen, E-Mails, Kiosks und andere Anzeigegeräte. Mit anderen Worten: Wenn Target-Bibliotheken und JavaScript nicht verwendet werden können, ermöglicht die [Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) weiterhin den Zugriff auf alle Target-Funktionen, um personalisierte Erlebnisse bereitzustellen.

>[!NOTE]
>
>Verwenden Sie beim Anfordern von Inhalten mit tatsächlichen Empfehlungen (empfohlene Produkte oder Elemente) die Target-Bereitstellungs-API.

Um Empfehlungen abzurufen, senden Sie einen POST-Aufruf zur Adobe Target-Bereitstellungs-API mit den entsprechenden Kontextinformationen, die eine Benutzer-ID (zur Verwendung mit profilspezifischen Empfehlungen wie den kürzlich angezeigten Elementen des Benutzers), einen relevanten Mbox-Namen, Mbox-Parameter, Profilparameter oder andere Attribute enthalten können. Die Antwort enthält empfohlene entity.ids (und möglicherweise andere Entitätsdaten) im JSON- oder HTML-Format, die dann auf dem Gerät angezeigt werden können.

Die [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) für Adobe Target stellt alle vorhandenen Funktionen bereit, die eine Standard-Target-Anfrage bereitstellt.

Die Bereitstellungs-API:

* Ermöglicht den RESTful-Abruf von Erlebnissen oder Angeboten für einen Standort und eine Zielgruppe.
* Erfordert keine Authentifizierung.
* Nur POSTs.
* Verarbeitet keine Cookies oder Umleitungsaufrufe.
* Erfordert oder erkennt keine „Benutzerrollen“. Es ruft einfach Inhalte ab oder meldet Ereignisse an Target Edge-Server.

Gehen Sie wie folgt vor, um mit der Bereitstellungs-API Target-Erlebnisse einschließlich Empfehlungen bereitzustellen:

1. Erstellen Sie eine Target-Aktivität (A/B, XT, AP oder Recommendations) mit dem formularbasierten Composer (nicht dem Visual Experience Composer).
1. Verwenden Sie die Bereitstellungs-API , um eine Antwort auf die Anfragen zu erhalten, die von der soeben erstellten Target-Aktivität generiert wurden.

&lt;!— F: Warum sind BEIDE Schritte dafür notwendig? Wenn Sie eine formularbasierte Empfehlung für eine Mbox definiert haben, worin besteht dann der Vorteil, dass die Bereitstellungs-API ebenfalls integriert wird, um Ergebnisse abzurufen? Warum können Sie die Ergebnisse nicht einfach mit dem formularbasierten Rec auf dem Zielgerät bereitstellen lassen?..?? A: Siehe den unten stehenden Anwendungsfall … Dies ist der Fall, wenn Sie die ausstehenden Ergebnisse „abfangen“ möchten, um mehr Aufgaben auszuführen, bevor Sie die Ergebnisse anzeigen. Dinge wie Echtzeit-Vergleiche zu Beständen. —>

## Erstellen einer Empfehlung mit dem formularbasierten Experience Composer

Um Empfehlungen zu erstellen, die mit der Bereitstellungs-API verwendet werden können, verwenden Sie den [formularbasierten Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

1. Erstellen und speichern Sie zunächst ein JSON-basiertes Design, das Sie in Ihrer Empfehlung verwenden können. Beispiel-JSON sowie Hintergrundinformationen dazu, wie JSON-Antworten bei der Konfiguration einer formularbasierten Aktivität zurückgegeben werden können, finden Sie in der Dokumentation unter [Erstellen von Empfehlungsentwürfen](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html). In diesem Beispiel trägt der Entwurf den Namen *Einfaches JSON.*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. Gehen Sie in Target zu **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Recommendations]** und klicken Sie dann auf **[!UICONTROL Form]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. Wählen Sie eine Eigenschaft aus und klicken Sie auf **[!UICONTROL Next]**.
1. Definieren Sie den Speicherort, an dem Benutzer die Antwort der Empfehlung erhalten sollen. Im folgenden Beispiel wird ein Speicherort namens *api_charter* verwendet. Wählen Sie Ihr zuvor erstelltes JSON-basiertes Design mit dem Namen *Einfaches JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. Speichern und aktivieren Sie die Empfehlung. Es wird Ergebnisse generieren. [Sobald die Ergebnisse fertig sind](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html) können Sie die Bereitstellungs-API verwenden, um sie abzurufen.

## Verwenden der Bereitstellungs-API

Die Syntax für die [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) lautet:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Beachten Sie, dass der Clientcode erforderlich ist. Zur Erinnerung: Ihr Clientcode befindet sich möglicherweise in Adobe Target, indem Sie zu **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]** navigieren. Beachten Sie den **Client-Code** im Abschnitt **Recommendations-API-**&quot;.
   ![client-code.png](assets/client-code.png)
1. Nachdem Sie Ihren Client-Code haben, erstellen Sie Ihren Bereitstellungs-API-Aufruf. Das folgende Beispiel beginnt mit den in der Sammlung &quot;[-API-Postman](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection) bereitgestellten **[!UICONTROL Web Batched Mboxes Delivery API Call]** und nimmt entsprechende Änderungen vor. Beispiel:
   * Die **browser**- und **address**-Objekte wurden aus dem **body** entfernt, da sie für Anwendungsfälle außerhalb von HTML nicht erforderlich sind
   * *api_charter* wird in diesem Beispiel als Standortname aufgeführt
   * entity.id wird angegeben, da diese Empfehlung auf Inhaltsähnlichkeit basiert, d. h., es muss ein aktueller Elementschlüssel an Target übergeben werden.
     ![server-side-delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Denken Sie daran, Ihre Abfrageparameter korrekt zu konfigurieren. Geben Sie beispielsweise bei Bedarf `{{CLIENT_CODE}}` an. &lt;!— F: In der aktualisierten Aufrufsyntax wird entity.id als profileParameter und nicht als mboxParameter aufgeführt, wie dies in älteren Versionen der Fall war. —> &lt;!— F: Altes Bild ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Alter Begleittext: „Beachten Sie, dass diese Empfehlung auf Inhalten basiert, die auf der entity.id basieren, die über mboxParameters gesendet wird.“ —>
     ![client-code3](assets/client-code3.png)
1. Senden Sie die Anfrage. Dies wird für den Speicherort *api_charter* ausgeführt, auf dem eine aktive Empfehlung ausgeführt wird, die mit Ihrem JSON-Design definiert wird und eine Liste empfohlener Entitäten ausgibt.
1. Sie erhalten eine Antwort, die auf dem JSON-Design basiert.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
Die Antwort enthält die Schlüssel-ID sowie die Entitäts-IDs der empfohlenen Entitäten.

Durch diese Verwendung der Bereitstellungs-API mit Recommendations können Sie zusätzliche Schritte ausführen, bevor Sie dem Besucher Recommendations auf dem Nicht-HTML-Gerät anzeigen. Sie können beispielsweise die Antwort von der Bereitstellungs-API verwenden, um eine zusätzliche Echtzeitsuche nach Entitätsattributdetails (Bestand, Preis, Bewertung usw.) aus einem anderen System (z. B. CMS, PIM oder E-Commerce-Plattform) durchzuführen, bevor die endgültigen Ergebnisse angezeigt werden.

Mit dem in diesem Handbuch beschriebenen Ansatz können Sie jede Anwendung dazu bringen, die Antwort von Target zu nutzen, um personalisierte Empfehlungen zu geben!

## Beispielimplementierungen

Die folgenden Ressourcen enthalten Beispiele für verschiedene Implementierungen, die nicht auf HTML ausgerichtet sind. Beachten Sie, dass jede Implementierung aufgrund des Systems und der beteiligten Geräte einzigartig ist.

| Ressource | Details |
| --- | --- |
| [Konfigurieren der Target-Erweiterung in Experience Platform Launch und Implementieren von Target-APIs](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Schritte zum Konfigurieren der Target-Erweiterung in Experience Platform Launch, Hinzufügen der Target-Erweiterung zu Ihrer App und Implementieren von Target-APIs, um Aktivitäten anzufordern, Angebote vorab abzurufen und in den visuellen Vorschaumodus zu wechseln. |
| [Adobe Target-Knoten-Client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Open-Source-Target Node.js SDK v1.0 |
| [Server-seitige Übersicht](../../implement/server-side/server-side-overview.md) | Informationen zu Server-seitigen Adobe Target-Bereitstellungs-APIs, Server-seitigen Batch-Bereitstellungs-APIs, Node.js-SDK und Adobe Target Recommendations-APIs. |
| [Adobe Campaign-Inhaltsempfehlungen in E-Mails](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Dieser Blog beschreibt, wie Sie Inhaltsempfehlungen in E-Mails über Adobe Target und Adobe I/O Runtime in Adobe Campaign nutzen können. |

## Verwalten des Recommendations-Setups mit APIs

In den meisten Fällen werden Empfehlungen in der Adobe Target-Benutzeroberfläche konfiguriert und dann über die Target-APIs verwendet oder aufgerufen, beispielsweise aus den in den obigen Abschnitten genannten Gründen. Diese UI-API-Koordination ist üblich. Manchmal möchten die Benutzer jedoch möglicherweise alle Aktionen über APIs durchführen - sowohl die Einrichtung als auch die Verwendung der Ergebnisse. Obwohl dies weniger häufig vorkommt, können Benutzer die Ergebnisse von Recommendations absolut konfigurieren *ausführen und* vollständig mithilfe der -APIs nutzen.

In einem [ Abschnitt haben wir gelernt](manage-catalog.md) wie Adobe Target Recommendations-Entitäten verwaltet und Server-seitig bereitgestellt werden. Ebenso können Sie mit der [Adobe Developer Console](https://developer.adobe.com/console/home) Kriterien, Promotions, Sammlungen und Design-Vorlagen verwalten, ohne sich bei Adobe Target anmelden zu müssen. Eine vollständige Liste aller Recommendations-APIs finden Sie [hier](https://developer.adobe.com/target/administer/recommendations-api/), aber hier finden Sie eine Zusammenfassung als Referenz.

| Ressource | Details |
| --- | --- |
| [Sammlungen](https://developer.adobe.com/target/administer/recommendations-api/#tag/Collections) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen von Sammlungen. |
| [Kriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Criteria) | Kriterien auflisten und abrufen. |
| [Designs](https://developer.adobe.com/target/administer/recommendations-api/#tag/Designs) | Auflisten, Erstellen, Abrufen, Bearbeiten, Löschen und Überprüfen von Designs. |
| [Entitäten](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities) | Speichern, Löschen und Abrufen von Entitäten. |
| [Promotions](https://developer.adobe.com/target/administer/recommendations-api/#tag/Promotions) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen von Promotions. |
| [Kategoriekriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Category-Criteria) | Kategoriekriterien auflisten, erstellen, abrufen, bearbeiten und löschen. |
| [Benutzerdefinierte Kriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Custom-Criteria) | Benutzerdefinierte Kriterien auflisten, erstellen, abrufen, bearbeiten und löschen. |
| [Elementkriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Item-Criteria) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen von Elementkriterien. |
| [Beliebtheitskriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Popularity-Criteria) | Popularitätskriterien auflisten, erstellen, abrufen, bearbeiten und löschen. |
| [Kriterien für Profilattribute](https://developer.adobe.com/target/administer/recommendations-api/#tag/Profile-Attribute-Criteria) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen von Profilattributkriterien. |
| [Aktuelle Kriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Recent-Criteria) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen der letzten Kriterien. |
| [Sequenzkriterien](https://developer.adobe.com/target/administer/recommendations-api/#tag/Sequence-Criteria) | Auflisten, Erstellen, Abrufen, Bearbeiten und Löschen von Sequenzkriterien. |

## Referenzdokumentation

* [Dokumentation zur Adobe Target-Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md)
* [Integration von Recommendations in E-Mail](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Zusammenfassung und Überprüfung

Herzlichen Glückwunsch! Durch den Abschluss dieses Handbuchs haben Sie Folgendes gelernt:
* [Verwalten des Katalogs mithilfe der Recommendations-API](manage-catalog.md)
* [Verwalten benutzerdefinierter Kriterien mithilfe der Recommendations-API](manage-custom-criteria.md)
* [Verwenden der Bereitstellungs-API mit Recommendations](fetch-recs-server-side-delivery-api.md)
