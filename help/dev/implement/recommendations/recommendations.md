---
keywords: Recommendations, Einstellungen, Voreinstellungen, vertikaler Markt, nicht mit Filtern kompatible Kriterien, Standard-Hostgruppe, Thumb-Basis-URL, Recommendations-API-Token, 9 USD
description: Erfahren Sie, wie Sie [!UICONTROL Recommendations] Aktivitäten in [!DNL Adobe Target].
title: Implementieren [!UICONTROL Recommendations] Aktivitäten?
feature: Recommendations
exl-id: af1e8b60-6dbb-451b-aa4f-e167d1800d1c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 29%

---

# Planung und Umsetzung [!UICONTROL Recommendations]

Informationen zur Planung und Implementierung [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Zusätzlich zu diesem Artikel wird die [Handbuch für Adobe Target Business Practices](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=de){target=_blank} contains in-depth information about [Target Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html){target=_blank}.

Vor der Einrichtung Ihrer ersten [!UICONTROL Recommendations] Aktivität in [!DNL Adobe Target]führen Sie die folgenden Schritte aus:

1. [Implementierung [!UICONTROL Target]](#implement-target) auf der Web- und mobilen App-Oberfläche, die Sie zur Erfassung des Benutzerverhaltens und zur Bereitstellung von Empfehlungen verwenden möchten.
1. [Richten Sie Ihre [!UICONTROL Recommendations] Katalog](#set-up-your-recommendations-catalog) von Produkten oder Inhalten, die Sie Ihren Benutzern empfehlen möchten.
1. [Übergeben von Verhaltensinformationen und -kontext](#pass-behavioral-information-and-context) nach [!DNL Target Recommendations] , damit sie personalisierte Empfehlungen bereitstellen kann.
1. [Konfigurieren globaler Ausnahmen](#configure-global-exclusions).
1. [Konfigurieren [!UICONTROL Recommendations] settings](#configure-recommendations-settings).
1. (Optional) [Verwaltung [!UICONTROL Recommendations] Verwenden von Admin-APIs](#administer-recommendations-using-admin-apis).

## 1. Umsetzung [!UICONTROL Target]

[!DNL Target Recommendations] erfordert die Implementierung des Adobe Experience Platform Web SDK oder at.js 0.9.2 (oder höher). Siehe [[!UICONTROL Target] Clientseitige Implementierungshandbücher](../client-side/overview.md) für weitere Informationen.

## 2. Richten Sie Ihre [!UICONTROL Recommendations] Katalog

Bereitstellung hochwertiger Empfehlungen, [!UICONTROL Target] muss über die Produkte oder Inhalte informiert sein, die Sie empfehlen möchten. Kataloge enthalten in der Regel drei Arten von Informationen zu empfohlenen Artikeln. Nehmen wir an, Sie empfehlen Filme. Fügen Sie Folgendes hinzu:

1. Daten, die dem Benutzer angezeigt werden sollen, der die Empfehlung erhält. Beispielsweise können Sie den Namen des Films und eine URL für ein Miniaturbild des Filmposters anzeigen.
1. Daten, die zur Anwendung von Marketing- und Merchandising-Steuerelementen nützlich sind. Beispielsweise können Sie die Filmanzeige so anzeigen, dass Sie keine Filme vom Typ NC-17 empfehlen.
1. Daten, die für die Bestimmung der Ähnlichkeit von Elementen mit anderen Elementen nützlich sind. Sie können beispielsweise das Genre des Films und den Regisseur des Films anzeigen.

[!UICONTROL Target] bietet mehrere Integrationsoptionen zum Ausfüllen Ihres Katalogs. Diese Optionen können zusammen verwendet werden, um verschiedene Elemente im Katalog zu aktualisieren oder um verschiedene Elementattribute auf unterschiedlichen Frequenzen zu aktualisieren.

| Methode | Was es ist | Einsatz | Zusätzliche Informationen |
| --- | --- | --- | --- |
| Katalog-Feed | Planen Sie einen Feed (CSV, Google Product XML oder Analytics Product Classifications), der täglich hochgeladen und erfasst werden soll. | Zum Senden von Informationen über mehrere Elemente gleichzeitig. Zum Senden von Informationen, die sich selten ändern. | Siehe [Feeds](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html). |
| Entitäts-API | Rufen Sie eine API auf, um Aktualisierungen für ein einzelnes Element in Minutenschnelle zu senden. | Zum Versand von Updates, wenn sie jeweils etwa einen Artikel betreffen. Zum Senden von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Entwicklerdokumentation für Entitäts-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Übergeben von Aktualisierungen auf der Seite | Senden Sie Aktualisierungen für ein einzelnes Element per JavaScript auf der Seite oder mithilfe der Bereitstellungs-API an die Minute. | Zum Versand von Updates, wenn sie jeweils etwa einen Artikel betreffen. Zum Senden von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Artikelansichten/Produktseiten](#item-views-or-product-pages) unten. |

Die meisten Kunden sollten mindestens einen Feed implementieren. Anschließend können Sie Ihren Feed mit Aktualisierungen für häufig geänderte Attribute oder Elemente ergänzen, indem Sie entweder die Entitäten-API oder die Seitenmethode verwenden.

## 3. Weitergeben von Verhaltensinformationen und -kontext

Die Verhaltensinformationen und -kontexte, die an [!UICONTROL Target] hängt von der Aktion ab, die Ihr Besucher durchführt und die häufig mit dem Seitentyp verknüpft ist, mit dem Ihr Besucher interagiert.

### Artikelansichten oder Produktseiten

Auf Seiten, auf denen ein Besucher ein einzelnes Element anzeigt, z. B. eine Produktdetailseite, sollten Sie die Identität des vom Besucher angesehenen Elements weitergeben. Sie sollten auch die detaillierteste Kategorie des Elements übergeben, das der Besucher anzeigt, um Filterempfehlungen für die aktuelle Kategorie zu ermöglichen.

Sie können auch bestimmte schnell wechselnde Attribute auf der Produktseite selbst übergeben. Sie können beispielsweise den Preis (`value`) und Lagerbestand/Lagerbestand.

#### Pass-Preis und Bestand

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

Wahrscheinlich möchten Sie Ihre Empfehlungen auf einer Kategorieseite auf Produkte oder Inhalte innerhalb dieser Kategorie beschränken. Stellen Sie dazu sicher, dass Sie die Identität der aktuell angezeigten Kategorie übergeben.

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

Auf einer Warenkorbseite können Sie Artikel basierend auf dem Inhalt des aktuellen Warenkorbs des Besuchers empfehlen. Übergeben Sie dazu die IDs aller Elemente im aktuellen Warenkorb des Besuchers mithilfe des speziellen Parameters `cartIds`.

#### Übergeben von aktuell im Warenkorb befindlichen Artikeln

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Weitere Informationen zu kartbasierten Empfehlungen finden Sie unter [Warenkorbbasiert](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based) im *[!DNL Adobe Target]Handbuch für Geschäftspraktiken*.

### Ausschließen von Artikeln, die sich bereits im Warenkorb des Besuchers befinden

Auf Seiten Ihrer gesamten Site können Sie einige Artikel aus Empfehlungen ausschließen. So können Sie beispielsweise keine Artikel empfehlen, die sich bereits im aktuellen Warenkorb des Besuchers befinden. Übergeben Sie dazu die IDs aller Elemente, die Sie ausschließen möchten, mithilfe des speziellen Parameters `excludedIds`.

#### Auszuschließende Elemente weitergeben

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Seiten zur Kauf-/Bestellbestätigung

Wenn ein Kaufereignis eintritt, geben Sie die Identität des/der gekauften Artikel weiter. Siehe [Konversions-Tracking](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) im [Implementieren von &quot;at.js&quot;> [!UICONTROL Target] ohne Tag-Manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) Artikel.

## 4. Konfigurieren globaler Ausnahmen

Schließen Sie alle Elemente auf globaler Ebene aus, die Sie einem Besucher nie empfehlen möchten. Siehe [Ausnahmen](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/exclusions.html) im *[!DNL Adobe Target]Handbuch für Geschäftspraktiken*.

## 5. Konfigurieren [!UICONTROL Recommendations] settings

Verwalten Sie Ihre Implementierung von [!UICONTROL Recommendations] mithilfe der Einstellungen.

Um auf die Optionen für **[!UICONTROL Recommendations-Einstellungen]** zuzugreifen, öffnen Sie Target in [!DNL Adobe Experience Cloud] und klicken Sie dann auf **[!UICONTROL Recommendations]** > **[!UICONTROL Einstellungen]**.

![ALT-Bild](assets/recs_settings.png)

Die folgenden Optionen sind verfügbar:

| Einstellung | Beschreibung |
|--- |--- |
| Benutzerdefinierte globale Mbox | (Optional) Geben Sie die benutzerdefinierte globale Mbox an, die für [!UICONTROL Target]-Aktivitäten verwendet wird. Standardmäßig wird die globale mbox, die von [!UICONTROL Target] verwendet wird, auch für [!UICONTROL Recommendations] verwendet.<P>Hinweis: Diese Option wird auf die Variable [!UICONTROL Target] **[!UICONTROL Administration]** Seite. Öffnen [!UICONTROL Target]Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]**. |
| Vertikaler Markt | Der vertikale Markt hilft Ihnen bei der Kategorisierung Ihrer Empfehlungskriterien. Diese Informationen helfen Mitgliedern Ihres Teams dabei, Kriterien zu finden, die für eine bestimmte Seite sinnvoll sind, z. B. Kriterien, die sich am besten für die Warenkorbseite oder für eine Medienseite eignen. |
| Inkompatible Kriterien filtern | Aktivieren Sie diese Option, um nur diejenigen Kriterien anzuzeigen, bei denen die ausgewählte Seite die erforderlichen Daten übermittelt. Nicht jedes Kriterium wird auf jeder Seite korrekt ausgeführt. Die Seite oder Mbox muss `entity.id` oder `entity.categoryId` für die aktuellen Element-/aktuellen Kategorieempfehlungen kompatibel sein. Allgemein ist es am besten, lediglich kompatible Kriterien anzuzeigen. Wenn Sie jedoch möchten, dass inkompatible Kriterien für die Aktivität verfügbar sind, deaktivieren Sie diese Option.<P>Es wird empfohlen, dass Sie diese Option deaktivieren, wenn Sie eine Tag-Management-Lösung verwenden.<P>Weitere Informationen zu dieser Option finden Sie unter [[!UICONTROL Recommendations] FAQs](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html) im *[!DNL Adobe Target]Handbuch für Geschäftspraktiken*. |
| Standard-Hostgruppe | Wählen Sie Ihre Standard-Hostgruppe aus.<P>Die Hostgruppe kann verwendet werden, um die verfügbaren Elemente in Ihrem Katalog für verschiedene Verwendungen zu trennen. Sie können beispielsweise Hostgruppen für Entwicklungs- und Produktionsumgebungen, unterschiedliche Marken oder unterschiedliche Länder verwenden. Standardmäßig basieren die Vorschauergebnisse in „Katalogsuche“, „Sammlungen“ und „Ausnahmen“ auf der Standardhostgruppe. (Mit dem Umgebungsfilter können Sie auch eine andere Hostgruppe auswählen, um die Ergebnisse in der Vorschau anzuzeigen.) Neu hinzugefügte Elemente sind standardmäßig in allen Hostgruppen verfügbar, es sei denn, beim Erstellen oder Aktualisieren des Elements wurde eine Umgebungs-ID angegeben. Bereitgestellte Empfehlungen hängen von der in der Anfrage angegebenen Hostgruppe ab.<P>Wenn Ihre Produkte nicht angezeigt werden, stellen Sie sicher, dass Sie die richtige Hostgruppe verwenden. Wenn Sie beispielsweise Ihre Empfehlung so festlegen, dass eine Staging-Umgebung verwendet wird, und Ihre Hostgruppe auf „Staging“ eingestellt ist, müssen Sie eventuell Ihre Erfassung in der Staging-Umgebung neu erstellen, damit die Angebote angezeigt werden. Um zu sehen, welche Produkte in jeder Umgebung verfügbar sind, verwenden Sie für jede Umgebung die Katalogsuche. Sie können auch eine Vorschau der Inhalte von [!UICONTROL Recommendations] Sammlungen und Ausschlüsse für eine ausgewählte Umgebung (Hostgruppe).<P>**Hinweis:** Nachdem Sie die ausgewählte Umgebung geändert haben, müssen Sie auf „Suchen“ klicken, um die zurückgegebenen Ergebnisse zu aktualisieren.<P> **[!UICONTROL Der Umgebungsfilter ist an den folgenden Orten in der Target-Benutzeroberfläche verfügbar:]**<ul><li>Katalogsuche (**[!UICONTROL Recommendations]** > **[!UICONTROL Katalogsuche]**)</li><li>Sammlung erstellen, Dialogfeld (**[!UICONTROL Recommendations]** > **[!UICONTROL Sammlungen]** > **[!UICONTROL Neu erstellen]**)</li><li>Sammlung aktualisieren -Dialogfeld (**[!UICONTROL Recommendations]** > **[!UICONTROL Sammlungen]** > **[!UICONTROL Bearbeiten]**)</li><li>Dialogfeld &quot;Ausschluss erstellen&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Ausnahmen]** > **[!UICONTROL Neu erstellen]**)</li><li>Dialogfeld &quot;Ausschluss aktualisieren&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Ausnahmen]** > **[!UICONTROL Bearbeiten]**)</li></ul>Weitere Informationen finden Sie unter [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) im *[!DNL Adobe Target]Handbuch für Geschäftspraktiken*. |
| Miniaturansicht Basis-URL | Durch Festlegen einer Basis-URL für Ihren Produktkatalog können Sie relative URLs verwenden, wenn Sie beim Ausfüllen Ihrer URL Miniaturen Ihrer Produkte angeben.<P>Beispiel:<P>`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`<P>legt eine URL fest, die relativ zur Basis-URL für Miniaturen ist. |
| [!UICONTROL Recommendations-API-Token] | Verwenden Sie dieses Token in [!UICONTROL Recommendations] API-Aufrufe, wie die Download-API. |

## 6. (Optional) Administration [!UICONTROL Recommendations] Verwenden von Admin-APIs

Siehe [Verwendung [!UICONTROL Recommendations] APIs](../../before-administer/recs-api/overview.md) Handbuch mit Anleitungen zum Konfigurieren und Verwenden des [!UICONTROL Target] Admin- und Bereitstellungs-APIs für [!UICONTROL Recommendations].
