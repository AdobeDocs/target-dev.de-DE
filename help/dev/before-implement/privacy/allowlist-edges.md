---
keywords: implementieren, implementieren, Whitelist, Whitelist, Zulassungsliste, Zulassungsliste, Edge, Edges, 9 USD
description: Zeigen Sie eine Liste von Hosts an, um Ihnen bei der Zulassungsliste von [!DNL Adobe Target] Edges zu helfen (geografisch verteilte Serving-Knoten, die optimale Antwortzeiten für Endbenutzer gewährleisten).
title: Wie kann ich Edge-Knoten in Zulassungslisten einteilen? [!DNL Target]
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 1583cfe8ea1009fd1df5c5a0e5f3f95f72daf2b9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Zulassungsliste [!DNL Target] Edge-Knoten

Informationen und eine aktuelle Liste von Hosts, die Ihnen helfen, [!DNL Adobe Target] Kanten in Zulassungsliste zu bringen.

Ein Vorteil ist eine geografisch verteilte Serving-Architektur, die Endbenutzern, die Inhalte anfordern, optimale Reaktionszeiten gewährleistet, unabhängig davon, wo sie sich befinden. Jeder Edge-Knoten verfügt über alle Informationen, die erforderlich sind, um auf die Inhaltsanforderung des Benutzers zu reagieren und Analysedaten zu dieser Anforderung zu verfolgen. Benutzeranforderungen werden an den nächsten Edge-Knoten weitergeleitet. Weitere Informationen finden Sie unter [Das Edge-Netzwerk](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Sie können bei Bedarf [!DNL Target] Edge-Knoten in Zulassungslisten eintragen.

>[!IMPORTANT]
>
>Neben der Zulassungsauflistung der IP-Adressen der NAT (Network Address Translation) von [!DNL Target] Edges und der im Artikel behandelten [!DNL Target] Edge-IP-Adressen sollten Sie auch alle [!DNL Adobe Analytics] IP-Adressblöcke auf die Zulassungsliste gesetzt haben.
>
>Weitere Informationen finden Sie unter [Alle IP-Adressblöcke von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} in der Dokumentation zu den *Adobe Analytics-Technotes*.
>
>Die [!DNL Adobe Target] -Infrastruktur wird aktualisiert und Kunden, die eine Zulassungsliste der Adressen wünschen, müssen beide IP-Sätze verwenden. Andernfalls werden Kunden beeinträchtigt, die serverseitige oder hybride Implementierungen verwenden, bei denen Target-API-Aufrufe zum Abrufen von Erlebnissen aus einem Netzwerk hinter einer Firewall stammen, die für die Verwendung einer Zulassungsliste konfiguriert ist.
>
>Alle in den beiden folgenden Tabellen aufgeführten Edge4 *x*-Adressen werden am 9. August 2023 aktualisiert.

## IP-Adressen von [!DNL Target] Edges für die Übersetzung von Netzwerkadressen (NAT)

Liste der Ausgangs-IP-Adressen von [!DNL Target] Edges. Zulassungslisten Sie diese IPs, wenn Sie planen, dass [!DNL Target] Ihre Dienste erreicht.

| Edge-Standort | Ausgehend-IP-Adressen |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<P>13 235 112,4 <P>52 66 66 192 |
| Edge42 (Tokio) | 52 69 55 232<P>43 206 61 43 <P>13 113 73 214 |
| Edge44 (Ostküste USA) | 54 164 192 223<P>52 86 86 203 <P>54 88 167 98 |
| Edge45 (Westküste USA) | 52 40 124 129<P>54 148 219 69 <P>54 189 208 212 |
| Edge46 (Sydney) | 54 253 144,4<P>54 66 198 142 <P>13 211 218 51 |
| Edge47 (Irland) | 52 208 136 136<P>54 170 28 19 <P>99 80 111 82 |
| Edge48 (Singapur) | 3,1 141,36<P>18 143 112 116 <P>52 76 61 44 |

## [!DNL Target] Edge-IP-Adressen

Liste der IP-Adressen von [!DNL Target] Edges. Zulassungsliste dieser IPs, wenn Sie API-Aufrufe an [!DNL Target] -Edges durchführen möchten.

Diese Liste ändert sich häufig, da die Lastenausgleichsmodule auf der Grundlage von Traffic-Profilen nach oben und unten skaliert werden.

| Edge-Standort | Domain | IP-Adressen |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(wobei CLIENTCODE Ihre [!DNL Target] Client-ID ist) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52 66 66 192<P>13 235 112,4 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 43 206 61 43<P>13 113 73 214<P>52 69 55 232 |
| Edge44 (Ostküste USA) | `mboxedge44.tt.omtrdc.net` | 54 88 167 98<P>54 164 192 223<P>52 86 86 203 |
| Edge45 (Westküste USA) | `mboxedge45.tt.omtrdc.net` | 52 40 124 129<P>54 148 219 69<P>54 189 208 212 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 54 66 198 142<P>54 253 144,4<P>13 211 218 51 |
| Edge47 (Irland) | `mboxedge47.tt.omtrdc.net` | 54 170 28 19<P>52 208 136 136<P>99 80 111 82 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 52 76 61 44<P>3,1 141,36<P>18 143 112 116 |

Da die Lastenausgleichsmodule Änderungen im Traffic-Profil erkennen, wird es nach oben oder unten skaliert. Die für den Elastic Load Balancing erforderliche Zeit kann je nach erkannten Änderungen zwischen 1 und 7 Minuten betragen. Wenn der Lastenausgleich skaliert wird, aktualisiert er den DNS-Eintrag mit der neuen Liste der IP-Adressen. Um sicherzustellen, dass Sie die erhöhte Kapazität nutzen, verwendet der Elastic Load Balancing eine TTL-Einstellung für den DNS-Eintrag von 60 Sekunden.
