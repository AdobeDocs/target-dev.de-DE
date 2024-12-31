---
keywords: Recommendations, Einstellungen, Voreinstellungen, Branche vertikal, inkompatible Kriterien filtern, Standard-Hostgruppe, Thumb-Basis-URL, Recommendations-API-Token,
description: Erfahren Sie, wie Sie [!UICONTROL Recommendations] Aktivitäten in implementieren [!DNL Adobe Target].
title: Wie implementiere ich [!UICONTROL Recommendations] Aktivitäten?
feature: Recommendations
hidefromtoc: true
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
source-git-commit: aa032255222d92aeddd7238922eb450f1b6b93a0
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 18%

---

# Planen und Implementieren von [!UICONTROL Recommendations]

Informationen zur Planung und Implementierung von [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Zusätzlich zu diesem Artikel enthält das [Handbuch für Adobe Target Business Practitioner](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} ausführliche Informationen zu [Target Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

Führen Sie vor der Einrichtung Ihrer ersten [!UICONTROL Recommendations] in [!DNL Adobe Target] die folgenden Schritte aus:

1. [Implementieren Sie [!UICONTROL Target]](#implement-target) auf den Oberflächen für Web und Mobile Apps, die Sie zur Erfassung des Benutzerverhaltens und zur Bereitstellung von Empfehlungen verwenden möchten.
1. [Richten Sie Ihren [!UICONTROL Recommendations] ein](#set-up-your-recommendations-catalog) von Produkten oder Inhalten, die Sie Ihren Benutzern empfehlen möchten.
1. [Übergeben Sie Verhaltensinformationen und Kontext](#pass-behavioral-information-and-context), um [!DNL Target Recommendations] zu ermöglichen, personalisierte Empfehlungen bereitzustellen.
1. [Konfigurieren globaler Ausschlüsse](#configure-global-exclusions).
1. [Konfigurieren Sie [!UICONTROL Recommendations] Einstellungen](#configure-recommendations-settings).
1. (Optional) [Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-](#administer-recommendations-using-admin-apis).

## 1. Implementieren von [!UICONTROL Target]

[!DNL Target Recommendations] müssen Sie [!DNL Adobe Experience Platform Web SDK] oder at.js 0.9.2 (oder höher) implementieren. Weitere Informationen finden Sie in den [[!UICONTROL Target] Client](../client-side/overview.md)seitigen Implementierungshandbüchern.

## 2. Einrichten des [!UICONTROL Recommendations]

Um hochwertige Empfehlungen zu geben, müssen [!UICONTROL Target] die Produkte oder Inhalte kennen, die Sie empfehlen möchten. Kataloge enthalten in der Regel drei Arten von Informationen zu empfohlenen Elementen. Angenommen, Sie empfehlen Filme. Folgendes einschließen:

1. Daten, die dem Benutzer angezeigt werden sollen, der die Empfehlung erhält. Sie können beispielsweise den Namen des Films und eine URL für ein Miniaturbild des Filmposters anzeigen.
1. Daten, die zur Anwendung von Marketing- und Merchandising-Steuerelementen nützlich sind. Beispielsweise können Sie die Bewertung des Films anzeigen, sodass Sie NC-17-Filme nicht empfehlen.
1. Daten, die für die Bestimmung der Ähnlichkeit von Elementen mit anderen Elementen nützlich sind. Sie können beispielsweise das Genre des Films und den Regisseur des Films anzeigen.

[!UICONTROL Target] bietet mehrere Integrationsoptionen zum Ausfüllen Ihres Katalogs. Diese Optionen können zusammen verwendet werden, um verschiedene Elemente im Katalog zu aktualisieren oder verschiedene Elementattribute mit unterschiedlichen Häufigkeiten zu aktualisieren.

| Methode | Was es ist | Einsatz | Zusätzliche Informationen |
| --- | --- | --- | --- |
| Katalog-Feed | Planen Sie einen Feed (CSV, [!DNL Google] Product XML oder [!UICONTROL Analytics Product Classifications]), der täglich hochgeladen und aufgenommen werden soll. | Zum Senden von Informationen über mehrere Elemente gleichzeitig. Für den Versand von Informationen, die sich selten ändern. | Siehe [Feeds](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds). |
| Entitäten-API | Rufen Sie eine API auf, um minutengenaue Aktualisierungen für ein einzelnes Element zu senden. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe Entwicklerdokumentation [ Entitäten-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| Weitergeben von Aktualisierungen auf der Seite | Senden Sie minutengenaue Aktualisierungen für ein einzelnes Element mit JavaScript auf der Seite oder mithilfe der Bereitstellungs-API. | Zum Senden von Aktualisierungen, wenn diese jeweils nur für ein Element erfolgen. Für den Versand von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Artikelansichten/Produktseiten](#item-views-or-product-pages) unten. |

Die meisten Kundinnen und Kunden sollten mindestens einen Feed implementieren. Anschließend können Sie Ihren Feed mit Aktualisierungen für häufig geänderte Attribute oder Elemente ergänzen, indem Sie entweder die Entitäten-API oder die On-the-Page-Methode verwenden.

## 3. Weitergabe von Verhaltensinformationen und -kontext

Die Verhaltensinformationen und der Kontext, den Sie an [!UICONTROL Target] übergeben sollten, hängen von der Aktion ab, die Ihr Besucher durchführt und die häufig mit der Art der Seite verbunden ist, mit der Ihr Besucher interagiert.

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

Wenn ein Kaufereignis auftritt, übergeben Sie die Identität des gekauften Artikels oder der gekauften Artikel. Siehe [Konversionen verfolgen](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) im Artikel [Bereitstellen von at.js > Implementieren von [!UICONTROL Target] ohne Tag-Manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md).

## 4. Konfigurieren globaler Ausschlüsse

Schließen Sie alle Elemente auf globaler Ebene aus, die Sie einem Besucher nie empfehlen möchten. Siehe [Ausschlüsse](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) im Handbuch für *[!DNL Adobe Target]Business Practices*.

## 5. Konfigurieren der [!UICONTROL Recommendations]

Verwalten Sie Ihre Implementierung von [!UICONTROL Recommendations] mithilfe der Einstellungen.

Um auf die **[!UICONTROL Recommendations Settings]** zuzugreifen, öffnen Sie [!DNL Target] im [!DNL Adobe Experience Cloud] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Seite mit Recommendations-Einstellungen](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Konfigurieren Sie die folgenden Optionen:

### [!UICONTROL Recommendations API Token]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Recommendations API Token] verfügbar:

#### [!UICONTROL Client code]

Die [!DNL Target] [!UICONTROL client code].

Wenn Sie Ihre [!UICONTROL client code] nicht kennen, klicken Sie in der [!DNL Target]-Benutzeroberfläche auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Der [!UICONTROL client code] wird im [!UICONTROL Account Details] Abschnitt angezeigt.

#### Authentifizierungstoken

Die [!DNL Adobe Target] Admin-APIs, einschließlich [!DNL Recommendations Admin]-APIs, werden durch Authentifizierung gesichert, um sicherzustellen, dass nur autorisierte Benutzer sie für den Zugriff auf [!DNL Adobe Target] verwenden. Verwenden Sie die [Adobe Developer Console](https://developer.adobe.com/console/home), um diese Authentifizierung für alle [!DNL Adobe Experience Cloud solutions] zu verwalten, einschließlich [!DNL Adobe Target].

Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung für Adobe Target-APIs](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Seien Sie beim Generieren eines neuen Authentifizierungs-Tokens vorsichtig. Das Generieren eines neuen Tokens führt dazu, dass API-Aufrufe mit dem aktuellen Token fehlschlagen. Aktualisieren Sie alle Skripte oder Anwendungen mit dem neuen generierten Authentifizierungstoken.

### Kriterien

Die Kenntnis der vertikalen Märkte Ihrer Website hilft Target bei der Auswahl der Kriterien für Ihre Empfehlungen.

Kriterien in [!DNL Recommendations] sind Regeln, die basierend auf einem vorab festgelegten Satz von Besucherverhalten bestimmen, welche Produkte oder Inhalte empfohlen werden sollen. Kriterien können auf beliebten Trends, dem aktuellen und vergangenen Verhalten eines Besuchers oder ähnlichen Produkten und Inhalten basieren. Sie können mehrere Empfehlungstypen untereinander testen, indem Sie mehrere Kriterien verwenden.

Weitere Informationen finden Sie unter [Kriterien](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} im *Handbuch für Adobe Target Business Practitioner.*

Die folgenden Einstellungen sind im Abschnitt [!UICONTROL Criteria] verfügbar:

#### [!UICONTROL Industry/Vertical]

Der vertikale Markt hilft Ihnen bei der Kategorisierung Ihrer Empfehlungskriterien. Diese Informationen helfen Mitgliedern Ihres Teams dabei, Kriterien zu finden, die für eine bestimmte Seite sinnvoll sind, z. B. Kriterien, die am besten für die Warenkorbseite oder für eine Medienseite geeignet sind.

Die folgenden Kategorien sind in der Dropdown-Liste verfügbar:

* Keine Personalization
* Einzelhandel/E-Commerce
* Lead-Generierung/B2B/Finanzdienstleistungen
* Medien/Verlagswesen

#### [!UICONTROL Filter Incompatible Criteria]

Aktivieren Sie diese Option, um nur diejenigen Kriterien anzuzeigen, bei denen die ausgewählte Seite die erforderlichen Daten übermittelt. Nicht alle Kriterien werden auf jeder Seite korrekt ausgeführt. Die Seite oder Mbox muss `entity.id` oder `entity.categoryId` übergeben werden, damit die aktuellen Element-/aktuellen Kategorieempfehlungen kompatibel sind.

Allgemein ist es am besten, lediglich kompatible Kriterien anzuzeigen. Wenn für die Aktivität jedoch inkompatible Kriterien verfügbar sein sollen, aktivieren Sie diese Option nicht.

Adobe empfiehlt, diese Option zu deaktivieren, wenn Sie eine Tag-Management-Lösung verwenden.

Weitere Informationen zu dieser Option finden Sie unter [[!UICONTROL Recommendations] häufig gestellten ](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} im Handbuch für *[!DNL Adobe Target]Business Practices*.

### [!UICONTROL Product Catalog]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Product Catalog] verfügbar:

#### [!UICONTROL Default Host Group]

Wählen Sie Ihre Standard-Hostgruppe aus.

Die Hostgruppe kann verwendet werden, um die verfügbaren Elemente in Ihrem Katalog für verschiedene Verwendungen zu trennen. Sie können beispielsweise Hostgruppen für Entwicklungs- und Produktionsumgebungen, unterschiedliche Marken oder unterschiedliche Länder verwenden. Standardmäßig basieren die Vorschauergebnisse in „Katalogsuche“, „Sammlungen“ und „Ausnahmen“ auf der Standardhostgruppe. (Sie können auch eine andere Hostgruppe auswählen, um Ergebnisse in der Vorschau anzuzeigen, indem Sie den Umgebungsfilter verwenden.) Standardmäßig sind neu hinzugefügte Elemente in allen Hostgruppen verfügbar, es sei denn, beim Erstellen oder Aktualisieren des Elements wird eine Umgebungs-ID angegeben. Bereitgestellte Empfehlungen hängen von der in der Anfrage angegebenen Hostgruppe ab.

Wenn Ihre Produkte nicht angezeigt werden, stellen Sie sicher, dass Sie die richtige Hostgruppe verwenden. Wenn Sie beispielsweise Ihre Empfehlung so festlegen, dass eine Staging-Umgebung verwendet wird, und Ihre Hostgruppe auf „Staging“ eingestellt ist, müssen Sie eventuell Ihre Erfassung in der Staging-Umgebung neu erstellen, damit die Angebote angezeigt werden. Um zu sehen, welche Produkte in jeder Umgebung verfügbar sind, verwenden Sie für jede Umgebung die Katalogsuche. Sie können auch eine Vorschau des Inhalts [!UICONTROL Recommendations] Sammlungen und Ausschlüsse für eine ausgewählte Umgebung (Hostgruppe) anzeigen.

>[!NOTE]
>
>Nachdem Sie die ausgewählte Umgebung geändert haben, müssen Sie auf **[!UICONTROL Search]** klicken, um die zurückgegebenen Ergebnisse zu aktualisieren.

Der **[!UICONTROL Environment]** ist an den folgenden Stellen in der Target-Benutzeroberfläche verfügbar:

* Katalogsuche (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* Sammlungen (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* Dialogfeld „Sammlung erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* Dialogfeld „Sammlung aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* Dialogfeld „Ausschluss erstellen“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* Dialogfeld „Ausschluss aktualisieren“ (**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

Weitere Informationen finden Sie unter [Hosts](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} im Handbuch für *[!DNL Adobe Target]Business Practices*.

#### [!UICONTROL Thumbnail Base]

Durch Festlegen einer Basis-URL für Ihren Produktkatalog können Sie relative URLs verwenden, wenn Sie beim Ausfüllen Ihrer URL Miniaturen Ihrer Produkte angeben.

Beispiel:

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

legt eine URL fest, die relativ zur Basis-URL für Miniaturen ist.

### [!UICONTROL Custom Attribute Key Configuration]

Stützen Sie Ihre Empfehlungen auf ein Element, das im Besucherprofil gespeichert ist. Beispiel: „Letzter Artikel zum Warenkorb hinzugefügt“ oder „Zuletzt angesehenes Video zu 90 % oder mehr angesehen“.

Klicken Sie auf **[!UICONTROL Add]** , um eine neue Konfiguration zu erstellen, geben Sie einen Namen für die Konfiguration an, wählen Sie das gewünschte Profilattribut aus und klicken Sie dann auf **[!UICONTROL Save]**.

## 6. (Optional) Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-APIs

Informationen zum Konfigurieren und Verwenden [ APIs für die [!UICONTROL Target]-Verwaltung ](../../before-administer/recs-api/overview.md) Bereitstellungs-APIs für [!UICONTROL Recommendations] finden Sie im praxisorientierten Handbuch zum Verwenden von [!UICONTROL Recommendations]-APIs .
