---
keywords: auf die Zulassungsliste setzen Implementierung, Whitelist, Whitelist,, Zulassungsliste, Edge, Edges, $9
description: Eine Liste von Hosts anzeigen, um Zulassungsliste-Edges  [!DNL Adobe Target]  unterstützen (geografisch verteilte Serving-Knoten, die Endbenutzern eine optimale Reaktionszeit bieten).
title: Wie werden  [!DNL Target] Edge-Knoten Auf die Zulassungsliste gesetzt?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Auf die Zulassungsliste setzen [!DNL Target] Edge-Knoten

Informationen und eine aktuelle Liste der Hosts, die Ihnen bei der Zulassungsliste [!DNL Adobe Target] Edges helfen.

Ein Edge ist eine geografisch verteilte Serving-Architektur, die Endbenutzern bei der Inhaltsanfrage optimale Reaktionszeiten bietet, unabhängig davon, wo sie sich befinden. Jeder Edge-Knoten verfügt über alle Informationen, die erforderlich sind, um auf die Inhaltsanfrage des Benutzers zu reagieren und Analysedaten zu dieser Anfrage zu verfolgen. Benutzeranfragen werden an den nächsten Edge-Knoten weitergeleitet. Weitere Informationen finden Sie unter [Das Edge-Netzwerk](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Bei Bedarf können [!DNL Target] Edge-Knoten auf die Zulassungsliste gesetzt werden.

>[!IMPORTANT]
>
>Zusätzlich zur Zulassungsauflistung auf die Zulassungsliste setzte der NAT-IP-Adressen (Network Address Translation) von [!DNL Target]-Edges und [!DNL Target]-Edge-IP-Adressen, die im Artikel behandelt werden, sollten Sie auch alle [!DNL Adobe Analytics]-IP-Adressblöcke hinzufügen.
>
>Weitere Informationen finden Sie unter [Alle Adobe Analytics-IP-Adressblöcke](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} in der Dokumentation *Technotes zu Adobe Analytics*.
>
>auf die Zulassungsliste setzen [!DNL Adobe Target] Infrastruktur wird aktualisiert, und Kunden, die Adressen ändern möchten, müssen beide IP-Sätze verwenden. Andernfalls hat dies Auswirkungen auf Kunden, die Server-seitige oder Hybridimplementierungen verwenden, bei denen Target-API-Aufrufe zum Abrufen von Erlebnissen aus einem Netzwerk hinter einer Firewall stammen, die für die Verwendung einer -Zulassungsliste konfiguriert ist.

Um den unterbrechungsfreien Zugriff auf [!DNL Target] über die [!DNL Experience Edge Connector] sicherzustellen, können Kunden ihre Netzwerkkonfigurationen aktualisieren, um Traffic zum Proxy-Service zuzulassen.

## Proxy-Service - Übersicht

* **Service-Endpunkt**: `https://tnt-web-proxy.adobe.io`.
* **Infrastruktur**: Gehostet auf der [!DNL Adobe] Ethos-Plattform.
* **Hinweis**: Dieser Service verwendet latenzbasiertes DNS-Routing und verlässt sich nicht auf statische IP-Adressen.

## CNAME-Ziele

Der Proxy-Service leitet den Traffic dynamisch über mehrere Regionen mithilfe von CNAME-Einträgen weiter. Dies sind die aktuellen Ziele:

| Edge-Speicherort | Ausgangs-IP-Adressen |
| --- | --- |
| Region | CNAME-Ziel |
| Europa (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| US East (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| US East (us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## Empfohlene Einträge für Zulassungslisten

Um eine zuverlässige Konnektivität sicherzustellen, müssen die folgenden Hostnamen auf die Zulassungsliste gesetzt werden:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## Optional: IP-Erkennung

Wenn Ihre Netzwerkrichtlinien eine IP-basierte Zulassungsauflistung erfordern, können Sie mit diesem Tool die aktuellen öffentlichen IP-Adressen anzeigen, die mit dem Proxy-Service verknüpft sind:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`