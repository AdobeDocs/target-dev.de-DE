---
keywords: auf die Zulassungsliste setzen Implementierung, Whitelist, Whitelist,, Zulassungsliste, Edge, Edges, $9
description: Eine Liste von Hosts anzeigen, um Zulassungsliste-Edges  [!DNL Adobe Target]  unterstützen (geografisch verteilte Serving-Knoten, die Endbenutzern eine optimale Reaktionszeit bieten).
title: Wie werden  [!DNL Target] Edge-Knoten Auf die Zulassungsliste gesetzt?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 1583cfe8ea1009fd1df5c5a0e5f3f95f72daf2b9
workflow-type: tm+mt
source-wordcount: '476'
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
>Weitere Informationen finden Sie unter [Alle Adobe Analytics-IP-Adressblöcke](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} in der Dokumentation *Technische Hinweise zu Adobe Analytics*.
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
