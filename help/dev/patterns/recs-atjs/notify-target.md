---
title: Target benachrichtigen
description: Stellen Sie sicher, dass alle Ereignisse, die von  [!DNL Target] verfolgt werden müssen, mit der trackEvent -Methode gesendet werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# Benachrichtigen [!DNL Target]

Durch Abschluss dieses Schritts wird sichergestellt, dass alle Ereignisse, die an [!DNL Adobe Target] gesendet werden müssen, mit der `trackEvent` -Methode gesendet werden.

Jedes Ereignis, das in [!DNL Target] verfolgt werden muss, kann ein primäres Konversionsereignis oder eine Erfolgsmetrik sein.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

## [!DNL Target]-Diagramm benachrichtigen {#diagram}

Die Schrittnummer in der folgenden Abbildung entspricht dem folgenden Abschnitt.

![Target-Diagramm benachrichtigen](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1: Fire [!DNL Adobe Target] Track API

Dieser Schritt hilft Ihnen dabei sicherzustellen, dass alle Ereignisse, die an [!DNL Target] gesendet werden müssen, mit der `trackEvent` -Methode gesendet werden.

+++Siehe Details

![Adobe Target Tracking-API-Diagramm auslösen](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Sie senden die im Abschnitt *Voraussetzungen* unten genannten Attribute zur Bestellkonvertierung. Der Name der Mbox spielt keine Rolle, bei der Konvertierung wird jedoch `orderConfirmPage` verwendet.

Sie müssen die Bestellkonvertierungsattribute nicht in diesen Aufruf aufnehmen. Diese Aufrufe zeichnen im Idealfall Erfolgsmetriken auf, die vor den wichtigsten Konversionsereignissen als Mini-Konversionsereignisse betrachtet werden können. `CardIds` muss auf Grundlage des `Add to Cart` -Ereignisses in auf dem Warenkorb basierende Empfehlungen enthalten sein.

**Voraussetzungen**

* Treffen Sie sich mit Ihrem Geschäftsteam, um alle Ereignisse zu identifizieren, die als Konversions- oder Erfolgsmetriken betrachtet werden können. Sie müssen auch das Konversionsereignis identifizieren, das den Umsatz generiert, damit diese Details zusammen mit den Ereignisdaten an [!DNL Target] gesendet werden können.
* Stellen Sie sicher, dass die folgenden Attribute in der Datenschicht verfügbar sind, damit Sie sie mit dem Konversionsereignis senden können. Das Konversionsereignis generiert Umsatz, z. B. einen Produktkauf oder das Ereignis &quot;Zum Warenkorb hinzufügen&quot;.

   * `productPurchaseId`: Produkt-IDs, die im Rahmen der Bestellung gekauft wurden. Trennen Sie mehrere Produkte durch Kommas.
   * `orderTotal`: Bestellen Sie die Gesamtsumme für den Kauf.
   * `orderId`: Bestell-ID des Kaufs.

  Die folgende Abbildung zeigt eine [Regel für  [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html){target=_blank}, die nur auf der Seite [!UICONTROL Confirmation] ausgelöst werden soll.

  ![Seite &quot;Aktionskonfiguration&quot;](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Wenn Sie ein Ereignis zum Hinzufügen zum Warenkorb verfolgen, senden Sie `cartIds` als Parameter. Eine kommagetrennte Liste von Produkt-IDs kann für `cardIds` übergeben werden.

**Lesungen**

* [adobe.target.trackEvent() -Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds für kartbasierte Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Aktionen**

* Verwenden Sie die `adobe.target-trackEvent()` -Methode, um alle Daten zu senden, die an [!DNL Target] gesendet werden müssen.
