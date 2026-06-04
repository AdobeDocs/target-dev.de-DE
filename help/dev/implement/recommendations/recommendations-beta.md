---
keywords: Recommendations, Einstellungen, Voreinstellungen, Branche, vertikale Filter, inkompatible Kriterien, Standard-Hostgruppe, Thumb-Basis-URL, Recommendations-API-Token,
description: Erfahren Sie, wie Sie [!UICONTROL Recommendations]-Aktivitäten in  [!DNL Adobe Target].
title: Wie implementiere ich [!UICONTROL Recommendations]-Aktivitäten?
feature: Recommendations
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
TQID: https://experienceleague.adobe.com/A7j0oJbyO3oei-a2l02I58o9I0vCPrRcqWC-QgQUxBo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 1734
ht-degree: 17%

---

# Planen und Implementieren [!UICONTROL Recommendations]

Informationen zur Planung und Implementierung von [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Zusätzlich zu diesem Artikel enthält das [Handbuch für Adobe Target Business Practitioner](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} ausführliche Informationen zu [Target Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

Bevor Sie Ihre erste [!UICONTROL Recommendations]-Aktivität in [!DNL Adobe Target] einrichten, führen Sie die folgenden Schritte aus:

1. [Target[!UICONTROL &#x200B; auf &#x200B;]](#implement-target) Oberflächen für Web und Mobile Apps implementieren, die Sie zur Erfassung des Benutzerverhaltens und zur Bereitstellung von Empfehlungen verwenden möchten.
1. [Richten Sie Ihren [!UICONTROL Recommendations]-Katalog](#set-up-your-recommendations-catalog) von Produkten oder Inhalten ein, die Sie Ihren Benutzern empfehlen möchten.
1. [Übergeben Sie Verhaltensinformationen und Kontext](#pass-behavioral-information-and-context), um [!DNL Target Recommendations] zu ermöglichen, personalisierte Empfehlungen bereitzustellen.
1. [Konfigurieren globaler Ausschlüsse](#configure-global-exclusions).
1. [Konfigurieren [!UICONTROL Recommendations] Einstellungen](#configure-recommendations-settings).
1. (Optional) [Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-APIs](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implementieren von [!UICONTROL Target]

[!DNL Target Recommendations] müssen Sie [!DNL Adobe Experience Platform Web SDK] oder at.js 0.9.2 (oder höher) implementieren. Weitere Informationen finden Sie [[!UICONTROL &#x200B; Client]seitigen Implementierungshandbüchern &#x200B;](../client-side/overview.md) Target .

## &#x200B;2. Einrichten des [!UICONTROL Recommendations]Katalogs

Um hochwertige Empfehlungen zu geben, [!UICONTROL Target] die Produkte oder Inhalte kennen, die Sie empfehlen möchten. Kataloge enthalten in der Regel drei Arten von Informationen zu empfohlenen Elementen. Angenommen, Sie empfehlen Filme. Folgendes einschließen:

1. Daten, die dem Benutzer angezeigt werden sollen, der die Empfehlung erhält. Sie können beispielsweise den Namen des Films und eine URL für ein Miniaturbild des Filmposters anzeigen.
1. Daten, die zur Anwendung von Marketing- und Merchandising-Steuerelementen nützlich sind. Beispielsweise können Sie die Bewertung des Films anzeigen, sodass Sie NC-17-Filme nicht empfehlen.
1. Daten, die für die Bestimmung der Ähnlichkeit von Elementen mit anderen Elementen nützlich sind. Sie können beispielsweise das Genre des Films und den Regisseur des Films anzeigen.

[!UICONTROL Target] bietet mehrere Integrationsoptionen zum Ausfüllen Ihres Katalogs. Diese Optionen können zusammen verwendet werden, um verschiedene Elemente im Katalog zu aktualisieren oder verschiedene Elementattribute mit unterschiedlichen Häufigkeiten zu aktualisieren.

| Methode | Was es ist | Einsatz | Zusätzliche Informationen |
| --- | --- | --- | --- |
| Katalog-Feed | Planen Sie einen Feed (CSV, [!DNL Google] Product XML oder [!UICONTROL Analytics Product Classifications]), der täglich hochgeladen und aufgenommen werden soll. | Zum Senden von Informationen über mehrere Elemente gleichzeitig. Für den Versand von Informationen, die sich selten ändern. | Siehe [Feeds](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds). |
| Entitäten-API | Rufen Sie eine API auf, um minutengenaue Aktualisierungen für ein einzelnes Element zu senden. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe Entwicklerdokumentation [&#x200B; Entitäten-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Weitergeben von Aktualisierungen auf der Seite | Senden Sie minutengenaue Aktualisierungen für ein einzelnes Element mit JavaScript auf der Seite oder mithilfe der Bereitstellungs-API. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Artikelansichten/Produktseiten](#item-views-or-product-pages) unten. |

Die meisten Kundinnen und Kunden sollten mindestens einen Feed implementieren. Anschließend können Sie Ihren Feed mit Aktualisierungen für häufig geänderte Attribute oder Elemente ergänzen, indem Sie entweder die Entitäten-API oder die On-the-Page-Methode verwenden.

## &#x200B;3. Übergeben von Verhaltensinformationen und Kontext

Die Verhaltensinformationen und der Kontext, den Sie an [!UICONTROL Target] übergeben sollten, hängen von der Aktion ab, die Ihr Besucher durchführt und die häufig mit dem Seitentyp verbunden ist, mit dem Ihr Besucher interagiert.

### Artikelansichten oder Produktseiten

Auf Seiten, auf denen ein Besucher ein einzelnes Element anzeigt, z. B. eine Produktdetailseite, sollten Sie die Identität des Elements übergeben, das der Besucher anzeigt. Übergeben Sie außerdem die detaillierteste Kategorie des Elements, das der Besucher anzeigt, um Filterempfehlungen für die aktuelle Kategorie zu ermöglichen.

Sie können auch bestimmte sich schnell ändernde Attribute auf der Produktseite selbst übergeben. Beispielsweise können Sie den Preis (`value`) und die Lagerbestände/Lagerbestände übergeben.

#### Bestehender Preis und Bestand

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### Kategorieansichten/Kategorieseiten

Auf einer Kategorieseite möchten Sie Ihre Empfehlungen wahrscheinlich auf Produkte oder Inhalte innerhalb dieser Kategorie beschränken. Stellen Sie dazu sicher, dass Sie die Identität der aktuell angezeigten Kategorie übergeben.

#### Aktuelle Kategorie übergeben

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### Hinzufügungen zum Warenkorb/Warenkorbansichten/Checkout-Seiten

Auf einer Warenkorbseite können Sie Artikel basierend auf dem Inhalt des aktuellen Warenkorbs des Besuchers empfehlen. Übergeben Sie dazu die IDs aller Artikel im aktuellen Warenkorb des Besuchers mithilfe des speziellen `cartIds`.

#### Artikel weiterleiten, die sich derzeit im Warenkorb befinden

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Weitere Informationen zu Warenkorb-basierten Empfehlungen finden Sie unter [Warenkorb-](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) im Handbuch für *[!DNL Adobe Target]Business Practices*.

### Ausschließen von Artikeln, die sich bereits im Warenkorb des Besuchers befinden

Auf Seiten in Ihrer Site können Sie einige Elemente aus Empfehlungen ausschließen. Beispielsweise möchten Sie möglicherweise keine Artikel empfehlen, die sich bereits im aktuellen Warenkorb des Besuchers befinden. Übergeben Sie dazu die IDs aller Elemente, die Sie mithilfe des speziellen `excludedIds` ausschließen möchten.

#### Auszuschließende Elemente weitergeben

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Bestellungen/Auftragsbestätigungsseiten

Wenn ein Kaufereignis auftritt, übergeben Sie die Identität des gekauften Artikels oder der gekauften Artikel. Siehe [Konversionen verfolgen](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) im Artikel [Bereitstellen von at.js > Implementieren von [!UICONTROL Target] ohne einen Tag-Manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

## &#x200B;4. Globale Ausschlüsse konfigurieren

Schließen Sie alle Elemente auf globaler Ebene aus, die Sie einem Besucher nie empfehlen möchten. Siehe [Ausschlüsse](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) im Handbuch für *[!DNL Adobe Target]Business Practices*.

## &#x200B;5. Konfigurieren der [!UICONTROL Recommendations]-Einstellungen

Verwalten Sie Ihre Implementierung von [!UICONTROL Recommendations] mithilfe der Einstellungen.

Um auf die Optionen **[!UICONTROL Recommendations]** zuzugreifen, öffnen Sie [!DNL Target] im [!DNL Adobe Experience Cloud] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Seite Recommendations-Einstellungen](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Konfigurieren Sie die folgenden Optionen:

### [!UICONTROL Recommendations-API-Token]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Recommendations API-Token] verfügbar:

#### [!UICONTROL Client-Code]

Der [!DNL Target] [!UICONTROL Clientcode].

Wenn Sie Ihren [!UICONTROL Client-Code] nicht kennen, klicken Sie in der [!DNL Target]-Benutzeroberfläche auf **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**. Der [!UICONTROL Clientcode] wird im Abschnitt [!UICONTROL Kontodetails] angezeigt.

#### Authentifizierungstoken

Die [!DNL Adobe Target] Admin-APIs, einschließlich [!DNL Recommendations Admin]-APIs, werden durch Authentifizierung gesichert, um sicherzustellen, dass nur autorisierte Benutzer sie für den Zugriff auf [!DNL Adobe Target] verwenden. Verwenden Sie die [Adobe Developer Console](https://developer.adobe.com/console/home), um diese Authentifizierung für alle [!DNL Adobe Experience Cloud solutions] zu verwalten, einschließlich [!DNL Adobe Target].

Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung für Adobe Target-APIs](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Seien Sie beim Generieren eines neuen Authentifizierungs-Tokens vorsichtig. Das Generieren eines neuen Tokens führt dazu, dass API-Aufrufe mit dem aktuellen Token fehlschlagen. Aktualisieren Sie alle Skripte oder Anwendungen mit dem neuen generierten Authentifizierungstoken.

### Kriterien

Die Kenntnis der vertikalen Märkte Ihrer Website hilft Target bei der Auswahl der Kriterien für Ihre Empfehlungen.

Kriterien in [!DNL Recommendations] sind Regeln, die basierend auf einem vorab festgelegten Satz von Besucherverhalten bestimmen, welche Produkte oder Inhalte empfohlen werden sollen. Die Kriterien können auf angesagten Trends, dem aktuellen und früheren Verhalten eines Besuchers oder auf ähnlichen Produkten und Inhalten basieren. Sie können mehrere Empfehlungstypen untereinander testen, indem Sie mehrere Kriterien verwenden.

Weitere Informationen finden Sie unter [Kriterien](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} im *Handbuch für Adobe Target Business Practitioner.*

Die folgenden Einstellungen sind im Abschnitt [!UICONTROL Kriterien] verfügbar:

#### [!UICONTROL Branche/Vertikal]

Der vertikale Markt hilft Ihnen bei der Kategorisierung Ihrer Empfehlungskriterien. Diese Informationen helfen Mitgliedern Ihres Teams dabei, Kriterien zu finden, die für eine bestimmte Seite sinnvoll sind, z. B. Kriterien, die am besten für die Warenkorbseite oder für eine Medienseite geeignet sind.

Die folgenden Kategorien sind in der Dropdown-Liste verfügbar:

* Keine Personalization
* Einzelhandel/E-Commerce
* Lead-Generierung/B2B/Finanzdienstleistungen
* Medien/Verlagswesen

#### [!UICONTROL Inkompatible Kriterien filtern]

Aktivieren Sie diese Option, um nur diejenigen Kriterien anzuzeigen, bei denen die ausgewählte Seite die erforderlichen Daten übermittelt. Nicht alle Kriterien werden auf jeder Seite korrekt ausgeführt. Die Seite oder Mbox muss `entity.id` oder `entity.categoryId` übergeben werden, damit die aktuellen Element-/aktuellen Kategorieempfehlungen kompatibel sind.

Allgemein ist es am besten, lediglich kompatible Kriterien anzuzeigen. Wenn für die Aktivität jedoch inkompatible Kriterien verfügbar sein sollen, aktivieren Sie diese Option nicht.

Adobe empfiehlt, diese Option bei Verwendung einer Tag-Management-Lösung zu deaktivieren.

Weitere Informationen zu dieser Option finden Sie unter [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} im *[!DNL Adobe Target]Business Practices Guide*.

### [!UICONTROL Produktkatalog]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Produktkatalog] verfügbar:

#### [!UICONTROL Standard-Hostgruppe]

Wählen Sie Ihre Standard-Hostgruppe aus.

Die Hostgruppe kann verwendet werden, um die verfügbaren Elemente in Ihrem Katalog für verschiedene Verwendungen zu trennen. Sie können beispielsweise Hostgruppen für Entwicklungs- und Produktionsumgebungen, unterschiedliche Marken oder unterschiedliche Länder verwenden. Standardmäßig basieren die Vorschauergebnisse in „Katalogsuche“, „Sammlungen“ und „Ausnahmen“ auf der Standardhostgruppe. (Sie können auch eine andere Hostgruppe auswählen, um Ergebnisse in der Vorschau anzuzeigen, indem Sie den Umgebungsfilter verwenden.) Standardmäßig sind neu hinzugefügte Elemente in allen Hostgruppen verfügbar, es sei denn, beim Erstellen oder Aktualisieren des Elements wird eine Umgebungs-ID angegeben. Bereitgestellte Empfehlungen hängen von der in der Anfrage angegebenen Hostgruppe ab.

Wenn Ihre Produkte nicht angezeigt werden, stellen Sie sicher, dass Sie die richtige Hostgruppe verwenden. Wenn Sie beispielsweise Ihre Empfehlung so festlegen, dass eine Staging-Umgebung verwendet wird, und Ihre Hostgruppe auf „Staging“ eingestellt ist, müssen Sie eventuell Ihre Erfassung in der Staging-Umgebung neu erstellen, damit die Angebote angezeigt werden. Um zu sehen, welche Produkte in jeder Umgebung verfügbar sind, verwenden Sie für jede Umgebung die Katalogsuche. Sie können auch eine Vorschau des Inhalts von [!UICONTROL Recommendations] Sammlungen und Ausschlüssen für eine ausgewählte Umgebung (Hostgruppe) anzeigen.

>[!NOTE]
>
>Nachdem Sie die ausgewählte Umgebung geändert haben, müssen Sie auf **[!UICONTROL Suchen]** klicken, um die zurückgegebenen Ergebnisse zu aktualisieren.

Der **[!UICONTROL Umgebung]**-Filter ist an den folgenden Stellen in der Target-Benutzeroberfläche verfügbar:

* Katalogsuche (**[!UICONTROL Recommendations]** > **[!UICONTROL Katalogsuche]**)
* Sammlungen (**[!UICONTROL Recommendations]** > **[!UICONTROL Sammlungen]**)
* Dialogfeld „Sammlung erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Sammlungen]** > **[!UICONTROL Sammlung erstellen]**)
* Dialogfeld „Sammlung aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Sammlungen]** > **[!UICONTROL Bearbeiten]**)
* Dialogfeld „Ausschluss erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Ausschlüsse]** > **[!UICONTROL Ausschluss erstellen]**)
* Dialogfeld „Ausschluss aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Ausschlüsse]** > **[!UICONTROL Bearbeiten]**)

Weitere Informationen finden Sie unter [Hosts](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} im Handbuch für *[!DNL Adobe Target]Business Practices*.

#### [!UICONTROL Miniaturansicht - Basis]

Durch Festlegen einer Basis-URL für Ihren Produktkatalog können Sie relative URLs verwenden, wenn Sie beim Ausfüllen Ihrer URL Miniaturen Ihrer Produkte angeben.

Beispiel:

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

legt eine URL fest, die relativ zur Basis-URL für Miniaturen ist.

### [!UICONTROL Konfiguration benutzerdefinierter Attributschlüssel]

Stützen Sie Ihre Empfehlungen auf ein Element, das im Besucherprofil gespeichert ist. Beispiel: „Letzter Artikel zum Warenkorb hinzugefügt“ oder „Zuletzt angesehenes Video zu 90 % oder mehr angesehen“.

Klicken Sie **[!UICONTROL Hinzufügen]**, um eine neue Konfiguration zu erstellen, geben Sie einen Namen für die Konfiguration an, wählen Sie das gewünschte Profilattribut aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

## &#x200B;6. (Optional) Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-APIs

Im praxisorientierten Handbuch [Verwenden von [!UICONTROL Recommendations]-APIs](../../before-administer/recs-api/overview.md) erfahren Sie, wie Sie die [!UICONTROL Target] Admin- und Bereitstellungs-APIs für [!UICONTROL Recommendations].
