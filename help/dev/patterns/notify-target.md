---
title: Target benachrichtigen
description: Stellen Sie sicher, dass alle Ereignisse, die verfolgt werden müssen [!DNL Target] werden mit der trackEvent -Methode gesendet.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 65cad3c558aa0f52c8007dcdb566c0ce3b29d8b7
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Benachrichtigen [!DNL Target]

Durch Abschluss dieses Schritts wird sichergestellt, dass alle Ereignisse, die an gesendet werden müssen [!DNL Adobe Target] werden mithilfe der Variablen `trackEvent` -Methode.

Alle Ereignisse, die verfolgt werden müssen [!DNL Target] kann ein primäres Konversionsereignis oder eine Erfolgsmetrik sein.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie in den Vollbildmodus zu erweitern.

## Benachrichtigen [!DNL Target] Diagramm {#diagram}

Die Schrittnummer in der folgenden Abbildung entspricht dem folgenden Abschnitt.

![Target-Diagramm benachrichtigen](/help/dev/patterns/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Feuer [!DNL Adobe Target] Tracking-API

Dieser Schritt hilft Ihnen dabei sicherzustellen, dass alle Ereignisse, die an gesendet werden müssen [!DNL Target] werden mithilfe der Variablen `trackEvent` -Methode.

++ + Siehe Details

![Adobe Target Track-API-Diagramm auslösen](/help/dev/patterns/assets/fire-adobe-target-track-api-diagram.png){width="100" zoomable="yes"}

Sie senden die im Abschnitt Voraussetzung unten aufgeführten Bestellkonvertierungsattribute. Der Name der Mbox spielt keine Rolle, die Konversion erfolgt jedoch zur Verwendung `orderConfirmPage`.

Sie müssen die Bestellkonvertierungsattribute nicht in diesen Aufruf aufnehmen. Diese Aufrufe zeichnen im Idealfall Erfolgsmetriken auf, die vor den wichtigsten Konversionsereignissen als Mini-Konversionsereignisse betrachtet werden können. `CardIds` muss in auf dem Warenkorb basierende Empfehlungen auf der Grundlage der `Add to Cart` -Ereignis.

**Voraussetzungen**

* Treffen Sie sich mit Ihrem Geschäftsteam, um alle Ereignisse zu identifizieren, die als Konversions- oder Erfolgsmetriken betrachtet werden können. Sie müssen auch das Konversionsereignis identifizieren, das Umsatz generiert, damit diese Details an [!DNL Target] zusammen mit den Ereignisdaten.
* Stellen Sie sicher, dass die folgenden Attribute in der Datenschicht verfügbar sind, damit Sie sie mit dem Konversionsereignis senden können. Das Konversionsereignis generiert Umsatz, z. B. einen Produktkauf oder das Ereignis &quot;Zum Warenkorb hinzufügen&quot;.

   * `productPurchaseId`: Produkt-IDs, die im Rahmen der Bestellung erworben wurden. Kommagetrennte mehrere Produkte.
   * `orderTotal`: Bestellsumme für den Kauf.
   * `orderId`: Bestell-ID des Kaufs.

* Wenn Sie ein Ereignis zum Hinzufügen zum Warenkorb verfolgen, senden Sie `cartIds` als Parameter. Eine kommagetrennte Liste von Produkt-IDs kann für `cardIds`.

**Lesungen**

* [adobe.target.trackEvent() -Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds für auf dem Warenkorb basierende Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**Aktionen**

* Verwendung `adobe.target-trackEvent()` -Methode zum Senden aller Daten, die an gesendet werden müssen [!DNL Target].







