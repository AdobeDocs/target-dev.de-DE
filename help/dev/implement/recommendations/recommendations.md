---
keywords: Recommendations, Einstellungen, Voreinstellungen, Branchen-Vertikal, nicht kompatible Kriterien filtern, Standard-Hostgruppe, Thumb-Basis-URL, Recommendations-API-Token, $9
description: Erfahren Sie, wie Sie [!UICONTROL Recommendations] Aktivitäten in implementieren [!DNL Adobe Target].
title: Wie implementiere ich [!UICONTROL Recommendations] Aktivitäten?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 21%

---

# Planen und Implementieren von [!UICONTROL Recommendations]

Informationen zur Planung und Implementierung von [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Zusätzlich zu diesem Artikel enthält das [Handbuch für Adobe Target Business Practitioner](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=de){target=_blank} ausführliche Informationen zu [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=de){target=_blank}.

Führen Sie vor der Einrichtung Ihrer ersten [!UICONTROL Recommendations] in [!DNL Adobe Target] die folgenden Schritte aus:

1. [Implementieren Sie [!UICONTROL Target]](#implement-target) auf den Oberflächen für Web und Mobile Apps, die Sie zur Erfassung des Benutzerverhaltens und zur Bereitstellung von Empfehlungen verwenden möchten.
1. [Richten Sie Ihren [!UICONTROL Recommendations] ein](#set-up-your-recommendations-catalog) von Produkten oder Inhalten, die Sie Ihren Benutzern empfehlen möchten.
1. [Übergeben Sie Verhaltensinformationen und Kontext](#pass-behavioral-information-and-context), um [!DNL Target Recommendations] zu ermöglichen, personalisierte Empfehlungen bereitzustellen.
1. [Konfigurieren globaler Ausschlüsse](#configure-global-exclusions).
1. [Konfigurieren Sie [!UICONTROL Recommendations] Einstellungen](#configure-recommendations-settings).
1. (Optional) [Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-](#administer-recommendations-using-admin-apis).

## &#x200B;1. Implementieren von [!UICONTROL Target]

[!DNL Target Recommendations] müssen Sie Adobe Experience Platform Web SDK oder at.js 0.9.2 (oder höher) implementieren. Weitere Informationen finden Sie in den [[!UICONTROL Target] Client](../client-side/overview.md)seitigen Implementierungshandbüchern.

## &#x200B;2. Einrichten des [!UICONTROL Recommendations]

Um hochwertige Empfehlungen zu geben, müssen [!UICONTROL Target] die Produkte oder Inhalte kennen, die Sie empfehlen möchten. Kataloge enthalten in der Regel drei Arten von Informationen zu empfohlenen Elementen. Angenommen, Sie empfehlen Filme. Folgendes einschließen:

1. Daten, die dem Benutzer angezeigt werden sollen, der die Empfehlung erhält. Sie können beispielsweise den Namen des Films und eine URL für ein Miniaturbild des Filmposters anzeigen.
1. Daten, die zur Anwendung von Marketing- und Merchandising-Steuerelementen nützlich sind. Beispielsweise können Sie die Bewertung des Films anzeigen, sodass Sie NC-17-Filme nicht empfehlen.
1. Daten, die für die Bestimmung der Ähnlichkeit von Elementen mit anderen Elementen nützlich sind. Sie können beispielsweise das Genre des Films und den Regisseur des Films anzeigen.

[!UICONTROL Target] bietet mehrere Integrationsoptionen zum Ausfüllen Ihres Katalogs. Diese Optionen können zusammen verwendet werden, um verschiedene Elemente im Katalog zu aktualisieren oder verschiedene Elementattribute mit unterschiedlichen Häufigkeiten zu aktualisieren.

| Methode | Was es ist | Einsatz | Zusätzliche Informationen |
| --- | --- | --- | --- |
| Katalog-Feed | Planen Sie einen Feed (CSV, Google Product XML oder Analytics Product Classifications), der täglich hochgeladen und aufgenommen werden soll. | Zum Senden von Informationen über mehrere Elemente gleichzeitig. Für den Versand von Informationen, die sich selten ändern. | Siehe [Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=de). |
| Entitäten-API | Rufen Sie eine API auf, um minutengenaue Aktualisierungen für ein einzelnes Element zu senden. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe Entwicklerdokumentation [ Entitäten-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Weitergeben von Aktualisierungen auf der Seite | Senden Sie minutengenaue Aktualisierungen für ein einzelnes Element mit JavaScript auf der Seite oder mithilfe der Bereitstellungs-API. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Artikelansichten/Produktseiten](#item-views-or-product-pages) unten. |

>[!IMPORTANT]
>
>Seien Sie vorsichtig, wenn Sie Ihre [!DNL Recommendations]-[!UICONTROL Catalog] über die [!DNL Delivery API] aktualisieren. Der [!DNL Delivery API] ist öffentlich. Vermeiden Sie es daher, ihn zum Ausfüllen anklickbarer Elemente in Ihrem Recommendations-Katalog zu verwenden. Dies kann zu ungültigen Inhalten führen und Ihren Katalog belasten.
>
>**Best Practices**: Verwenden Sie die [!DNL Delivery API] nur zum Aktualisieren von Katalogattributen, die:
>
>* sich häufig ändern (z. B. Preis, Lagerbestand).
>
>* Verwenden Sie ein vordefiniertes Format, das auf Ihrer Website einfach validiert werden kann.
>
>* Verwenden Sie sie nicht zum Hinzufügen oder Ändern anklickbarer Elemente oder anderer nicht verifizierter Inhalte.
>
>* Bei Bedarf können Sie den Kunden-Support anfordern, um Katalogaktualisierungen über die Bereitstellungs-API zu deaktivieren.
>
>Weitere Informationen finden Sie in der [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}.

Die meisten Kundinnen und Kunden sollten mindestens einen Feed implementieren. Anschließend können Sie Ihren Feed mit Aktualisierungen für häufig geänderte Attribute oder Elemente ergänzen, indem Sie entweder die Entitäten-API oder die On-the-Page-Methode verwenden.

## &#x200B;3. Weitergabe von Verhaltensinformationen und -kontext

Die Verhaltensinformationen und der Kontext, den Sie an [!UICONTROL Target] übergeben sollten, hängen von der Aktion ab, die Ihr Besucher durchführt und die häufig mit der Art der Seite verbunden ist, mit der Ihr Besucher interagiert.

### Artikelansichten oder Produktseiten

Auf Seiten, auf denen ein Besucher ein einzelnes Element anzeigt, z. B. eine Produktdetailseite, sollten Sie die Identität des Elements übergeben, das der Besucher anzeigt. Sie sollten auch die detaillierteste Kategorie des Elements übergeben, das der Besucher anzeigt, um Filterempfehlungen für die aktuelle Kategorie zu ermöglichen.

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

Weitere Informationen zu Warenkorb-basierten Empfehlungen finden Sie unter [Warenkorb-](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=de#cart-based) im Handbuch für *[!DNL Adobe Target]Business Practices*.

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

Wenn ein Kaufereignis auftritt, übergeben Sie die Identität des gekauften Artikels oder der gekauften Artikel. Siehe [Konversionen verfolgen](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) im Artikel [Bereitstellen von at.js > Implementieren von [!UICONTROL Target] ohne Tag-Manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) .

## &#x200B;4. Konfigurieren globaler Ausschlüsse

Schließen Sie alle Elemente auf globaler Ebene aus, die Sie einem Besucher nie empfehlen möchten. Siehe [Ausschlüsse](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html?lang=de) im Handbuch für *[!DNL Adobe Target]Business Practices*.

## &#x200B;5. Konfigurieren der [!UICONTROL Recommendations]

Verwalten Sie Ihre Implementierung von [!UICONTROL Recommendations] mithilfe der Einstellungen.

Um auf die **[!UICONTROL Recommendations Settings]** Optionen zuzugreifen, öffnen Sie Target im [!DNL Adobe Experience Cloud] und klicken Sie dann auf **[!UICONTROL Recommendations]** > **[!UICONTROL Settings]**.

![Seite Recommendations-Einstellungen](/help/dev/implement/recommendations/assets/recs_settings.png)

Die folgenden Optionen sind verfügbar:

| Einstellung | Beschreibung |
|--- |--- |
| Benutzerdefinierte globale Mbox | (Optional) Geben Sie die benutzerdefinierte globale Mbox an, die für [!UICONTROL Target]-Aktivitäten verwendet wird. Standardmäßig wird die von [!UICONTROL Target] verwendete globale Mbox für die [!UICONTROL Recommendations] verwendet.<P>Hinweis: Diese Option wird auf der Seite [!UICONTROL Target] **[!UICONTROL Administration]** festgelegt. Öffnen Sie [!UICONTROL Target] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Vertikaler Markt | Der vertikale Markt hilft Ihnen bei der Kategorisierung Ihrer Empfehlungskriterien. Diese Informationen helfen Mitgliedern Ihres Teams dabei, Kriterien zu finden, die für eine bestimmte Seite sinnvoll sind, z. B. Kriterien, die am besten für die Warenkorbseite oder für eine Medienseite geeignet sind. |
| Inkompatible Kriterien filtern | Aktivieren Sie diese Option, um nur diejenigen Kriterien anzuzeigen, bei denen die ausgewählte Seite die erforderlichen Daten übermittelt. Nicht alle Kriterien werden auf jeder Seite korrekt ausgeführt. Die Seite oder Mbox muss `entity.id` oder `entity.categoryId` übergeben werden, damit die aktuellen Element-/aktuellen Kategorieempfehlungen kompatibel sind. Allgemein ist es am besten, lediglich kompatible Kriterien anzuzeigen. Wenn Sie jedoch möchten, dass inkompatible Kriterien für die Aktivität verfügbar sind, deaktivieren Sie diese Option.<P>Es wird empfohlen, dass Sie diese Option deaktivieren, wenn Sie eine Tag-Management-Lösung verwenden.<P>Weitere Informationen zu dieser Option finden Sie unter [[!UICONTROL Recommendations] häufig gestellten ](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=de) im Handbuch für *[!DNL Adobe Target]Business Practices*. |
| Standard-Hostgruppe | Wählen Sie Ihre Standard-Hostgruppe aus.<P>Die Hostgruppe kann verwendet werden, um die verfügbaren Elemente in Ihrem Katalog für verschiedene Verwendungen zu trennen. Sie können beispielsweise Hostgruppen für Entwicklungs- und Produktionsumgebungen, unterschiedliche Marken oder unterschiedliche Länder verwenden. Standardmäßig basieren die Vorschauergebnisse in „Katalogsuche“, „Sammlungen“ und „Ausnahmen“ auf der Standardhostgruppe. (Sie können auch eine andere Hostgruppe auswählen, um Ergebnisse in der Vorschau anzuzeigen, indem Sie den Umgebungsfilter verwenden.) Standardmäßig sind neu hinzugefügte Elemente in allen Hostgruppen verfügbar, es sei denn, beim Erstellen oder Aktualisieren des Elements wird eine Umgebungs-ID angegeben. Bereitgestellte Empfehlungen hängen von der in der Anfrage angegebenen Hostgruppe ab.<P>Wenn Ihre Produkte nicht angezeigt werden, stellen Sie sicher, dass Sie die richtige Hostgruppe verwenden. Wenn Sie beispielsweise Ihre Empfehlung so festlegen, dass eine Staging-Umgebung verwendet wird, und Ihre Hostgruppe auf „Staging“ eingestellt ist, müssen Sie eventuell Ihre Erfassung in der Staging-Umgebung neu erstellen, damit die Angebote angezeigt werden. Um zu sehen, welche Produkte in jeder Umgebung verfügbar sind, verwenden Sie für jede Umgebung die Katalogsuche. Sie können auch eine Vorschau des Inhalts [!UICONTROL Recommendations] Sammlungen und Ausschlüsse für eine ausgewählte Umgebung (Hostgruppe) anzeigen.<P>**Hinweis:** Nachdem Sie die ausgewählte Umgebung geändert haben, müssen Sie auf „Suchen“ klicken, um die zurückgegebenen Ergebnisse zu aktualisieren.<P> **[!UICONTROL The Environment]** Filter ist an den folgenden Stellen in der Target-Benutzeroberfläche verfügbar:<ul><li>Katalogsuche (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)</li><li>Dialogfeld „Sammlung erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create New]**)</li><li>Dialogfeld „Sammlung aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)</li><li>Dialogfeld „Ausschluss erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create New]**)</li><li>Dialogfeld „Ausschluss aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)</li></ul>Weitere Informationen finden Sie unter [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=de) im Handbuch für *[!DNL Adobe Target]Business Practices*. |
| Miniaturansicht Basis-URL | Durch Festlegen einer Basis-URL für Ihren Produktkatalog können Sie relative URLs verwenden, wenn Sie beim Ausfüllen Ihrer URL Miniaturen Ihrer Produkte angeben.<P>Beispiel:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>legt eine URL fest, die relativ zur Basis-URL für Miniaturen ist. |
| API-Token [!UICONTROL Recommendations] | Verwenden Sie dieses Token in [!UICONTROL Recommendations] API-Aufrufen, z. B. in der Download-API. |

## &#x200B;6. (Optional) Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-APIs

Informationen zum Konfigurieren und Verwenden [ APIs für die [!UICONTROL Recommendations]-Verwaltung ](../../before-administer/recs-api/overview.md) Bereitstellungs-APIs für [!UICONTROL Target] finden Sie im praxisorientierten Handbuch zum Verwenden von [!UICONTROL Recommendations]-APIs .
