---
keywords: Implementierung, Whitelist, Whitelist,, Zulassungsliste, Edge, Edges, $9
description: Eine Liste von Hosts anzeigen, um Zulassungsliste-Edges  [!DNL Adobe Target]  unterstützen (geografisch verteilte Serving-Knoten, die Endbenutzern eine optimale Reaktionszeit bieten).
title: Wie werden  [!DNL Target] Edge-Knoten Auf die Zulassungsliste gesetzt?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
TQID: https://experienceleague.adobe.com/-XCVJpuvQ1xV9vQBZbomDKU3F-60b5FS-LU8lIBp4GQ
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 373
ht-degree: 0%

---

# [!DNL Target] Edge-Knoten

Informationen und eine aktuelle Liste der Hosts, die Ihnen bei der Zulassungsliste [!DNL Adobe Target] Edges helfen.

Ein Edge ist eine geografisch verteilte Serving-Architektur, die Endbenutzern bei der Inhaltsanfrage optimale Reaktionszeiten bietet, unabhängig davon, wo sie sich befinden. Jeder Edge-Knoten verfügt über alle Informationen, die erforderlich sind, um auf die Inhaltsanfrage des Benutzers zu reagieren und Analysedaten zu dieser Anfrage zu verfolgen. Benutzeranfragen werden an den nächsten Edge-Knoten weitergeleitet. Weitere Informationen finden Sie unter [Das Edge-Netzwerk](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=de#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Bei Bedarf können [!DNL Target] Edge-Knoten auf die Zulassungsliste gesetzt werden.

>[!IMPORTANT]
>
>Zusätzlich zur Zulassungsauflistung der NAT-IP-Adressen (Network Address Translation) von [!DNL Target]-Edges und [!DNL Target]-Edge-IP-Adressen, die im Artikel behandelt werden, sollten Sie auch alle [!DNL Adobe Analytics]-IP-Adressblöcke hinzufügen.
>
>Weitere Informationen finden Sie unter [Alle Adobe Analytics-IP-Adressblöcke](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=de#all-adobe-analytics-ip-address-blocks){target=_blank} in der Dokumentation *Technotes zu Adobe Analytics*.
>
>[!DNL Adobe Target] Infrastruktur wird aktualisiert, und Kunden, die Adressen ändern möchten, müssen beide IP-Sätze verwenden. Andernfalls hat dies Auswirkungen auf Kunden, die Server-seitige oder Hybridimplementierungen verwenden, bei denen Target-API-Aufrufe zum Abrufen von Erlebnissen aus einem Netzwerk hinter einer Firewall stammen, die für die Verwendung einer -Zulassungsliste konfiguriert ist.

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