---
title: Zielgruppe benachrichtigen
description: Stellen Sie sicher, dass alle Ereignisse, die verfolgt werden müssen [!DNL Target]  mit der trackEvent-Methode gesendet werden.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# [!DNL Target] benachrichtigen

Durch Abschluss dieses Schritts wird sichergestellt, dass alle Ereignisse, die an [!DNL Adobe Target] gesendet werden müssen, mit der `trackEvent`-Methode gesendet werden.

Jedes Ereignis, das in verfolgt werden muss, [!DNL Target] ein primäres Konversionsereignis oder eine Erfolgsmetrik sein.

>[!TIP]
>
>Klicken Sie auf die Bilder in diesem Thema, um sie im Vollbildmodus anzuzeigen.

## Benachrichtigen [!DNL Target] Diagramms {#diagram}

Die Schrittnummer in der folgenden Abbildung entspricht dem folgenden Abschnitt.

![Target-Diagramm benachrichtigen](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1: Fire [!DNL Adobe Target] Track-API

Mit diesem Schritt können Sie sicherstellen, dass alle Ereignisse, die an [!DNL Target] gesendet werden müssen, mit der `trackEvent`-Methode gesendet werden.

+++Siehe Details

![Diagramm zur Fire Adobe Target Track-API](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

Sie senden die Attribute für die Auftragskonvertierung wie im Abschnitt *Voraussetzungen* unten beschrieben. Der Name der Mbox spielt keine Rolle, die Konvertierung besteht jedoch in der Verwendung von `orderConfirmPage`.

Sie müssen die Attribute für die Bestellkonvertierung nicht in diesen Aufruf einbeziehen. Diese Aufrufe zeichnen idealerweise Erfolgsmetriken auf, die vor den Hauptkonversionsereignissen als Mini-Konversionsereignisse betrachtet werden können. `CardIds` müssen in auf dem Warenkorb basierende Empfehlungen auf der Grundlage des `Add to Cart`-Ereignisses enthalten sein.

**Voraussetzungen**

* Treffen Sie sich mit Ihrem Business-Team, um alle Ereignisse zu identifizieren, die als Konversions- oder Erfolgsmetriken betrachtet werden können. Sie müssen auch das Konversionsereignis identifizieren, das Umsatz generiert, damit diese Details zusammen mit den Ereignisdaten an [!DNL Target] gesendet werden können.
* Stellen Sie sicher, dass die folgenden Attribute in der Datenschicht verfügbar sind, damit Sie sie mit dem Konversionsereignis senden können. Das Konversionsereignis generiert Umsatz, z. B. ein Produktkauf- oder Warenkorbereignis.

   * `productPurchaseId`: Produkt-IDs, die im Rahmen der Bestellung gekauft wurden. Trennen Sie mehrere Produkte durch Kommas.
   * `orderTotal`: Bestellsumme für den Kauf.
   * `orderId`: Auftrags-ID des Kaufs.

  Die folgende Abbildung zeigt eine [Regel für [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html?lang=de){target=_blank}, die nur auf der [!UICONTROL Confirmation]-Seite ausgelöst werden sollte.

  ![Seite „Aktionskonfiguration“](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* Wenn Sie ein Ereignis für das Hinzufügen zum Warenkorb verfolgen, senden Sie `cartIds` als Parameter. Eine kommagetrennte Liste von Produkt-IDs kann für `cardIds` übergeben werden.

**Messwerte**

* [adobe.target.trackEvent()-Methode](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [cartIds für auf dem Warenkorb basierende Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=de#cart-based){target=_blank}

**Aktionen**

* Verwenden Sie `adobe.target-trackEvent()` -Methode, um alle Daten zu senden, die an [!DNL Target] gesendet werden müssen.
