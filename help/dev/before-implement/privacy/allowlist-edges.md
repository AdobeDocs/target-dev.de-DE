---
keywords: auf die Zulassungsliste setzen Implementierung, Whitelist, Whitelist,, Zulassungsliste, Edge, Edges, $9
description: Eine Liste von Hosts anzeigen, um Zulassungsliste-Edges  [!DNL Adobe Target]  unterstützen (geografisch verteilte Serving-Knoten, die Endbenutzern eine optimale Reaktionszeit bieten).
title: Wie werden  [!DNL Target] Edge-Knoten Auf die Zulassungsliste gesetzt?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 275c3fabdcaf3152d7d6161f3c325e54c840c805
workflow-type: tm+mt
source-wordcount: '563'
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
>
>Alle Edge *4.x*-Adressen, die in den beiden folgenden Tabellen aufgeführt sind, werden voraussichtlich am 9. August 2023 aktualisiert.

## Network Address Translation (NAT) - IP-Adressen von [!DNL Target]

Liste der Ausgangs-IP-Adressen [!DNL Target] Edge. Zulassungsliste dieser IPs, wenn Sie [!DNL Target] Ihre Services kontaktieren möchten.

| Edge-Speicherort | Ausgangs-IP-Adressen |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 (Tokio) | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44 (Ostküste der USA) | 54.164.192.223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45 (Westküste der USA) | 52.40.124.129<P>54.148.219.69 <P>54.189.208.212 |
| Edge46 (Sydney) | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 (Irland) | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 (Singapur) | 3.1.141.36<P>18.143.112.116 <P>52.76.61.44 |

## [!DNL Target] Edge-IP-Adressen

Liste der IP-Adressen der [!DNL Target]. Zulassungsliste dieser IPs, wenn Sie API-Aufrufe an [!DNL Target] Edges durchführen möchten.

Diese Liste ändert sich häufig, da die Lastenausgleichsmodule basierend auf Traffic-Profilen hoch- und herunterskaliert werden.

| Edge-Speicherort | Domain | IP-Adressen |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(wobei CLIENTCODE Ihre [!DNL Target] Client-ID ist) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44 (Ostküste der USA) | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54.164.192.223<P>52.86.86.203 |
| Edge45 (Westküste der USA) | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54.148.219.69<P>54.189.208.212 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 (Irland) | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18.143.112.116 |

Wenn die Lastenausgleichsmodule Änderungen am Traffic-Profil erkennen, werden sie nach oben oder unten skaliert. Die Zeit, die für den elastischen Lastausgleich benötigt wird, um zu skalieren, kann je nach den erkannten Änderungen zwischen 1 und 7 Minuten liegen. Wenn die Load-Balancer skaliert werden, aktualisieren sie den DNS-Eintrag mit der neuen Liste der IP-Adressen. Um sicherzustellen, dass Sie die erhöhte Kapazität nutzen, verwendet Elastic Load Balancing eine TTL-Einstellung für den DNS-Eintrag von 60 Sekunden.

## Zulassungsauflistung der Anforderungen für [!DNL Target] Proxy-Service

Um den unterbrechungsfreien Zugriff auf [!DNL Target] über den [!DNL Experience Edge Connector] (EEC) sicherzustellen, müssen Kunden möglicherweise ihre Netzwerkkonfigurationen aktualisieren, um Traffic zum Proxy-Service zuzulassen.

### Proxy-Service - Übersicht

* **Service-Endpunkt**: `https://tnt-web-proxy.adobe.io`.
* **Infrastruktur**: Gehostet auf der [!DNL Adobe] Ethos-Plattform.
* **Hinweis**: Dieser Service verwendet latenzbasiertes DNS-Routing und verlässt sich nicht auf statische IP-Adressen.

### CNAME-Ziele

Der Proxy-Service leitet den Traffic dynamisch über mehrere Regionen mithilfe von CNAME-Einträgen weiter. Dies sind die aktuellen Ziele:

| Edge-Speicherort | Ausgangs-IP-Adressen |
| --- | --- |
| Region | CNAME-Ziel |
| Europa (eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| US East (us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| US East (us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

### Empfohlene Einträge für Zulassungslisten

Um eine zuverlässige Konnektivität sicherzustellen, müssen die folgenden Hostnamen auf die Zulassungsliste gesetzt werden:

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

### Optional: IP-Erkennung

Wenn Ihre Netzwerkrichtlinien eine IP-basierte Zulassungsauflistung erfordern, können Sie mit diesem Tool die aktuellen öffentlichen IP-Adressen anzeigen, die mit dem Proxy-Service verknüpft sind:

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`