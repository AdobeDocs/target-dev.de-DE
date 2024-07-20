---
keywords: Recommendations, Einstellungen, Voreinstellungen, vertikaler Markt, nicht mit Filtern kompatible Kriterien, Standard-Hostgruppe, Thumb-Basis-URL, Recommendations-API-Token,
description: Erfahren Sie, wie Sie [!UICONTROL Recommendations] -Aktivitäten in  [!DNL Adobe Target] implementieren.
title: Wie implementiere ich [!UICONTROL Recommendations] -Aktivitäten?
feature: Recommendations
hidefromtoc: true
hide: true
exl-id: 0a9c9649-195b-44e2-987e-d02eaf98cc54
source-git-commit: aa032255222d92aeddd7238922eb450f1b6b93a0
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 20%

---

# Planen und Implementieren von [!UICONTROL Recommendations]

Informationen zur Planung und Implementierung von [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>Zusätzlich zu diesem Artikel enthält der [Adobe Target Business Practitioner Guide](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} ausführliche Informationen zu [Target Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

Führen Sie die folgenden Schritte aus, bevor Sie Ihre erste [!UICONTROL Recommendations] -Aktivität in [!DNL Adobe Target] einrichten:

1. [Implementieren Sie [!UICONTROL Target]](#implement-target) auf den Web- und mobilen App-Oberflächen, die Sie zur Erfassung des Benutzerverhaltens und zur Bereitstellung von Empfehlungen verwenden möchten.
1. [Richten Sie Ihren [!UICONTROL Recommendations] Katalog](#set-up-your-recommendations-catalog) mit Produkten oder Inhalten ein, die Sie Ihren Benutzern empfehlen möchten.
1. [Übergeben Sie Verhaltensinformationen und -kontext](#pass-behavioral-information-and-context) an [!DNL Target Recommendations], damit personalisierte Empfehlungen bereitgestellt werden können.
1. [Konfigurieren globaler Ausnahmen](#configure-global-exclusions).
1. [Konfigurieren Sie [!UICONTROL Recommendations] settings](#configure-recommendations-settings).
1. (Optional) [Verwalten Sie [!UICONTROL Recommendations] mithilfe von Admin-APIs](#administer-recommendations-using-admin-apis).

## 1. Implementierung von [!UICONTROL Target]

[!DNL Target Recommendations] erfordert die Implementierung von [!DNL Adobe Experience Platform Web SDK] oder at.js 0.9.2 (oder höher). Weitere Informationen finden Sie in den [[!UICONTROL Target] clientseitigen Implementierungshandbüchern](../client-side/overview.md) .

## 2. Richten Sie Ihren [!UICONTROL Recommendations]-Katalog ein.

Um Empfehlungen von hoher Qualität bereitzustellen, muss [!UICONTROL Target] über die Produkte oder Inhalte Bescheid wissen, die Sie empfehlen möchten. Kataloge enthalten in der Regel drei Arten von Informationen zu empfohlenen Artikeln. Nehmen wir an, Sie empfehlen Filme. Fügen Sie Folgendes hinzu:

1. Daten, die dem Benutzer angezeigt werden sollen, der die Empfehlung erhält. Beispielsweise können Sie den Namen des Films und eine URL für ein Miniaturbild des Filmposters anzeigen.
1. Daten, die zur Anwendung von Marketing- und Merchandising-Steuerelementen nützlich sind. Beispielsweise können Sie die Filmanzeige so anzeigen, dass Sie keine Filme vom Typ NC-17 empfehlen.
1. Daten, die für die Bestimmung der Ähnlichkeit von Elementen mit anderen Elementen nützlich sind. Sie können beispielsweise das Genre des Films und den Regisseur des Films anzeigen.

[!UICONTROL Target] bietet mehrere Integrationsoptionen zum Ausfüllen Ihres Katalogs. Diese Optionen können zusammen verwendet werden, um verschiedene Elemente im Katalog zu aktualisieren oder um verschiedene Elementattribute auf unterschiedlichen Frequenzen zu aktualisieren.

| Methode | Was es ist | Einsatz | Zusätzliche Informationen |
| --- | --- | --- | --- |
| Katalog-Feed | Planen Sie, dass ein Feed (CSV, [!DNL Google] Produkt-XML oder [!UICONTROL Analytics Product Classifications]) täglich hochgeladen und erfasst wird. | Zum Senden von Informationen über mehrere Elemente gleichzeitig. Zum Senden von Informationen, die sich selten ändern. | Siehe [Feeds](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds). |
| Entitäts-API | Rufen Sie eine API auf, um Aktualisierungen für ein einzelnes Element in Minutenschnelle zu senden. | Zum Versand von Updates, wenn sie jeweils etwa einen Artikel betreffen. Zum Senden von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Weitere Informationen finden Sie in der Entwicklerdokumentation für die [Entitäts-API](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities) . |
| Übergeben von Aktualisierungen auf der Seite | Senden Sie über JavaScript auf der Seite oder die Bereitstellungs-API Aktualisierungen für ein einzelnes Element in Minutenschnelle. | Zum Versand von Updates, wenn sie jeweils etwa einen Artikel betreffen. Zum Senden von Informationen, die sich häufig ändern (z. B. Preis, Bestand/Lagerbestand). | Siehe [Artikelansichten/Produktseiten](#item-views-or-product-pages) unten. |

Die meisten Kunden sollten mindestens einen Feed implementieren. Anschließend können Sie Ihren Feed mit Aktualisierungen für häufig geänderte Attribute oder Elemente ergänzen, indem Sie entweder die Entitäten-API oder die Seitenmethode verwenden.

## 3. Weitergeben von Verhaltensinformationen und -kontext

Die Verhaltensinformationen und der Kontext, die an [!UICONTROL Target] weitergegeben werden sollen, hängen von der Aktion ab, die Ihr Besucher unternimmt und die häufig mit dem Seitentyp verknüpft ist, mit dem Ihr Besucher interagiert.

### Artikelansichten oder Produktseiten

Auf Seiten, auf denen ein Besucher ein einzelnes Element anzeigt, z. B. eine Produktdetailseite, sollten Sie die Identität des vom Besucher angesehenen Elements weitergeben. Übergeben Sie außerdem die detaillierteste Kategorie des Elements, das der Besucher anzeigt, um Filterempfehlungen für die aktuelle Kategorie zu ermöglichen.

Sie können auch bestimmte schnell wechselnde Attribute auf der Produktseite selbst übergeben. Sie können beispielsweise den Preis (`value`) und das Bestand-/Lagerniveau überschreiben.

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

Auf einer Warenkorbseite können Sie Artikel basierend auf dem Inhalt des aktuellen Warenkorbs des Besuchers empfehlen. Übergeben Sie dazu die IDs aller Elemente im aktuellen Warenkorb des Besuchers mit dem speziellen Parameter `cartIds`.

#### Übergeben von aktuell im Warenkorb befindlichen Artikeln

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

Weitere Informationen zu kartbasierten Empfehlungen finden Sie unter [Warenkorbbasiert](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) im *[!DNL Adobe Target]Business-Practice-Handbuch*.

### Ausschließen von Artikeln, die sich bereits im Warenkorb des Besuchers befinden

Auf Seiten Ihrer gesamten Site können Sie einige Artikel aus Empfehlungen ausschließen. So können Sie beispielsweise keine Artikel empfehlen, die sich bereits im aktuellen Warenkorb des Besuchers befinden. Übergeben Sie dazu die IDs aller Elemente, die Sie ausschließen möchten, mit dem Sonderparameter `excludedIds`.

#### Auszuschließende Elemente weitergeben

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### Seiten zur Kauf-/Bestellbestätigung

Wenn ein Kaufereignis eintritt, geben Sie die Identität des/der gekauften Artikel weiter. Siehe [Konversions-Tracking](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) im Artikel [Bereitstellen von at.js > Implementieren von [!UICONTROL Target] ohne Tag-Manager](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) .

## 4. Konfigurieren globaler Ausnahmen

Schließen Sie alle Elemente auf globaler Ebene aus, die Sie einem Besucher nie empfehlen möchten. Siehe [Ausschlüsse](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) im *[!DNL Adobe Target]Business-Practice-Handbuch*.

## 5. [!UICONTROL Recommendations] Einstellungen konfigurieren

Verwalten Sie Ihre Implementierung von [!UICONTROL Recommendations] mithilfe der Einstellungen.

Um auf die **[!UICONTROL Recommendations Settings]** -Optionen zuzugreifen, öffnen Sie [!DNL Target] in der [!DNL Adobe Experience Cloud] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![Recommendations-Einstellungsseite](/help/dev/implement/recommendations/assets/recs-settings-new.png)

Konfigurieren Sie die folgenden Optionen:

### [!UICONTROL Recommendations API Token]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Recommendations API Token] verfügbar:

#### [!UICONTROL Client code]

Die [!DNL Target] [!UICONTROL client code].

Wenn Sie Ihren [!UICONTROL client code] nicht kennen, klicken Sie in der [!DNL Target] -Benutzeroberfläche auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. Die [!UICONTROL client code] wird im Abschnitt [!UICONTROL Account Details] angezeigt.

#### Authentifizierungstoken

Die [!DNL Adobe Target] Admin-APIs, einschließlich der [!DNL Recommendations Admin] -APIs, werden durch Authentifizierung gesichert, um sicherzustellen, dass nur autorisierte Benutzer sie für den Zugriff auf [!DNL Adobe Target] verwenden. Verwenden Sie den [Adobe Developer Console](https://developer.adobe.com/console/home) , um diese Authentifizierung für alle [!DNL Adobe Experience Cloud solutions], einschließlich [!DNL Adobe Target], zu verwalten.

Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung für Adobe Target-APIs](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>Seien Sie beim Generieren eines neuen Authentifizierungstokens vorsichtig. Das Generieren eines neuen Tokens führt dazu, dass API-Aufrufe mit dem aktuellen Token fehlschlagen. Aktualisieren Sie alle Skripte oder Anwendungen mit dem neuen generierten Authentifizierungstoken.

### Kriterien

Wenn Sie die Branche Ihrer Site kennen, hilft Target bei der Auswahl von Kriterien für Ihre Empfehlungen.

Kriterien in [!DNL Recommendations] sind Regeln, die anhand vorab ermittelter Verhaltensweisen von Besuchern festlegen, welche Produkte oder Inhalte empfohlen werden. Kriterien können auf beliebten Trends, dem aktuellen und früheren Verhalten eines Besuchers oder ähnlichen Produkten und Inhalten basieren. Sie können mehrere Empfehlungstypen untereinander testen, indem Sie mehrere Kriterien verwenden.

Weitere Informationen finden Sie unter [Kriterien](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} im *Adobe Target Business Practices-Handbuch.*

Die folgenden Einstellungen sind im Abschnitt [!UICONTROL Criteria] verfügbar:

#### [!UICONTROL Industry/Vertical]

Der vertikale Markt hilft Ihnen bei der Kategorisierung Ihrer Empfehlungskriterien. Diese Informationen helfen Mitgliedern Ihres Teams dabei, Kriterien zu finden, die für eine bestimmte Seite sinnvoll sind, z. B. Kriterien, die sich am besten für die Warenkorbseite oder für eine Medienseite eignen.

Die folgenden Kategorien sind in der Dropdown-Liste verfügbar:

* Kein Personalization
* Einzelhandel/E-Commerce
* Lead-Generierung/B2B/Finanzdienstleistungen
* Medien/Verlagswesen

#### [!UICONTROL Filter Incompatible Criteria]

Aktivieren Sie diese Option, um nur diejenigen Kriterien anzuzeigen, bei denen die ausgewählte Seite die erforderlichen Daten übermittelt. Nicht jedes Kriterium wird auf jeder Seite korrekt ausgeführt. Die Seite oder Mbox muss `entity.id` oder `entity.categoryId` für die aktuellen Element-/aktuellen Kategorieempfehlungen übergeben, um kompatibel zu sein.

Allgemein ist es am besten, lediglich kompatible Kriterien anzuzeigen. Wenn Sie jedoch möchten, dass inkompatible Kriterien für die Aktivität verfügbar sind, aktivieren Sie diese Option nicht.

Adobe empfiehlt, diese Option bei Verwendung einer Tag-Management-Lösung zu deaktivieren.

Weitere Informationen zu dieser Option finden Sie unter [[!UICONTROL Recommendations] FAQ](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} im *[!DNL Adobe Target]Handbuch für Geschäftspraktiker*.

### [!UICONTROL Product Catalog]

Die folgenden Optionen sind im Abschnitt [!UICONTROL Product Catalog] verfügbar:

#### [!UICONTROL Default Host Group]

Wählen Sie Ihre standardmäßige Hostgruppe aus.

Die Hostgruppe kann verwendet werden, um die verfügbaren Elemente in Ihrem Katalog für verschiedene Verwendungen zu trennen. Sie können beispielsweise Hostgruppen für Entwicklungs- und Produktionsumgebungen, unterschiedliche Marken oder unterschiedliche Länder verwenden. Standardmäßig basieren die Vorschauergebnisse in „Katalogsuche“, „Sammlungen“ und „Ausnahmen“ auf der Standardhostgruppe. (Mit dem Umgebungsfilter können Sie auch eine andere Hostgruppe auswählen, um die Ergebnisse in der Vorschau anzuzeigen.) Neu hinzugefügte Elemente sind standardmäßig in allen Hostgruppen verfügbar, es sei denn, beim Erstellen oder Aktualisieren des Elements wurde eine Umgebungs-ID angegeben. Bereitgestellte Empfehlungen hängen von der in der Anfrage angegebenen Hostgruppe ab.

Wenn Ihre Produkte nicht angezeigt werden, stellen Sie sicher, dass Sie die richtige Hostgruppe verwenden. Wenn Sie beispielsweise Ihre Empfehlung so festlegen, dass eine Staging-Umgebung verwendet wird, und Ihre Hostgruppe auf „Staging“ eingestellt ist, müssen Sie eventuell Ihre Erfassung in der Staging-Umgebung neu erstellen, damit die Angebote angezeigt werden. Um zu sehen, welche Produkte in jeder Umgebung verfügbar sind, verwenden Sie für jede Umgebung die Katalogsuche. Sie können auch eine Vorschau des Inhalts von [!UICONTROL Recommendations] Sammlungen und Ausschlüssen für eine ausgewählte Umgebung (Hostgruppe) anzeigen.

>[!NOTE]
>
>Nachdem Sie die ausgewählte Umgebung geändert haben, müssen Sie auf **[!UICONTROL Search]** klicken, um die zurückgegebenen Ergebnisse zu aktualisieren.

Der Filter **[!UICONTROL Environment]** ist an den folgenden Stellen in der Target-Benutzeroberfläche verfügbar:

* Katalogsuche (**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* Sammlungen (**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* Dialogfeld &quot;Sammlung erstellen&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* Dialogfeld &quot;Sammlung aktualisieren&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* Dialogfeld &quot;Ausschluss erstellen&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* Dialogfeld &quot;Ausschluss aktualisieren&quot;(**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

Weitere Informationen finden Sie unter [Hosts](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} im *[!DNL Adobe Target]Business-Practice-Handbuch*.

#### [!UICONTROL Thumbnail Base]

Durch Festlegen einer Basis-URL für Ihren Produktkatalog können Sie relative URLs verwenden, wenn Sie beim Ausfüllen Ihrer URL Miniaturen Ihrer Produkte angeben.

Beispiel:

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

legt eine URL fest, die relativ zur Basis-URL für Miniaturen ist.

### [!UICONTROL Custom Attribute Key Configuration]

Stützen Sie Ihre Empfehlungen auf einen Artikel, der im Besucherprofil gespeichert ist. Beispiel: &quot;Letzter Artikel zum Warenkorb hinzugefügt&quot;oder &quot;Letztes Video, das mindestens 90 % angesehen hat&quot;.

Klicken Sie auf **[!UICONTROL Add]** , um eine neue Konfiguration zu erstellen, geben Sie einen Namen für die Konfiguration an, wählen Sie das gewünschte Profilattribut aus und klicken Sie dann auf **[!UICONTROL Save]**.

## 6. (Optional) Verwalten von [!UICONTROL Recommendations] mithilfe von Admin-APIs

Weitere Informationen zum Konfigurieren und Verwenden der [!UICONTROL Target] Admin- und Bereitstellungs-APIs für [!UICONTROL Recommendations] finden Sie im Handbuch [Verwenden von [!UICONTROL Recommendations] APIs](../../before-administer/recs-api/overview.md) .
