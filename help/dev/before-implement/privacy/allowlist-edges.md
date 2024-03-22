---
keywords: implementieren, implementieren, Whitelist, Whitelist, Zulassungsliste, Zulassungsliste, Edge, Edges, 9 USD
description: Anzeigen einer Liste von Hosts, die Ihnen bei der Zulassungsliste des  helfen [!DNL Adobe Target] Edges (geografisch verteilte Serving-Knoten, die optimale Reaktionszeiten für Endbenutzer gewährleisten).
title: Wie kann ich eine Zulassungsliste vornehmen? [!DNL Target] Edge-Knoten?
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 49b6572c0d414ab304712691c97794bb0b1e3781
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Zulassungsliste [!DNL Target] Edge-Knoten

Informationen und eine aktuelle Liste von Hosts, die Ihnen bei der Zulassungsliste von helfen [!DNL Adobe Target] Kanten.

Ein Vorteil ist eine geografisch verteilte Serving-Architektur, die Endbenutzern, die Inhalte anfordern, optimale Reaktionszeiten gewährleistet, unabhängig davon, wo sie sich befinden. Jeder Edge-Knoten verfügt über alle Informationen, die erforderlich sind, um auf die Inhaltsanforderung des Benutzers zu reagieren und Analysedaten zu dieser Anforderung zu verfolgen. Benutzeranforderungen werden an den nächsten Edge-Knoten weitergeleitet. Weitere Informationen finden Sie unter [Edge Network](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934).

Sie können eine Zulassungsliste [!DNL Target] Kantenknoten, falls gewünscht.

>[!IMPORTANT]
>
>Zusätzlich zur Zulassungsauflistung der NAT-IP-Adressen (Network Address Translation) von [!DNL Target] Kanten und [!DNL Target] Edge-IP-Adressen, die im Artikel besprochen werden, sollten Sie auch alle Zulassungslisten [!DNL Adobe Analytics] IP-Adressblöcke.
>
>Weitere Informationen finden Sie unter [Alle IP-Adressblöcke von Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank} im *Technische Hinweise zu Adobe Analytics* Dokumentation.
>
>[!DNL Adobe Target] Die Infrastruktur wird aktualisiert und Kunden, die die Adressen in Zulassungslisten eintragen möchten, müssen beide IP-Sätze verwenden. Andernfalls werden Kunden beeinträchtigt, die serverseitige oder hybride Implementierungen verwenden, bei denen Target-API-Aufrufe zum Abrufen von Erlebnissen aus einem Netzwerk hinter einer Firewall stammen, die für die Verwendung einer Zulassungsliste konfiguriert ist.
>
>Alle Edge4 *x* Die Adressen, die in den beiden folgenden Tabellen aufgeführt sind, sollen am 9. August 2023 aktualisiert werden.

## IP-Adressen der NAT (Network Address Translation) von [!DNL Target] Kanten

Liste der ausgehenden IP-Adressen von [!DNL Target] Kanten. Wenn Sie planen, diese IPs von Auf die Zulassungsliste setzen zu erhalten [!DNL Target] Wenden Sie sich an Ihre Dienste.

| Edge-Standort | Ausgehend-IP-Adressen |
| --- | --- |
| Edge41 (Mumbai) | 3.6.2.221<br />13 235 112,4 <br />52 66 66 192 |
| Edge42 (Tokio) | 52 69 55 232<br />43 206 61 43 <br />13 113 73 214 |
| Edge44 (Ostküste USA) | 54 164 192 223<br />52 86 86 203 <br />54 88 167 98 |
| Edge45 (Westküste USA) | 52 40 124 129<br />54 148 219 69 <br />54 189 208 212 |
| Edge46 (Sydney) | 54 253 144,4<br />54 66 198 142 <br />13 211 218 51 |
| Edge47 (Irland) | 52 208 136 136<br />54 170 28 19 <br />99 80 111 82 |
| Edge48 (Singapur) | 3,1 141,36<br />18 143 112 116 <br />52 76 61 44 |

## [!DNL Target] Edge-IP-Adressen

Liste der IP-Adressen von [!DNL Target] Kanten. Zulassungsliste dieser IPs, wenn Sie API-Aufrufe an senden möchten [!DNL Target] Kanten.

Diese Liste ändert sich häufig, da die Lastenausgleichsmodule auf der Grundlage von Traffic-Profilen nach oben und unten skaliert werden.

| Edge-Standort | Domain | IP-Adressen |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />(wobei CLIENTCODE Ihre [!DNL Target] Client-ID) |  |
| Edge41 (Mumbai) | `mboxedge41.tt.omtrdc.net` | 15.206.104.6<br />3 109 14 178 <br />13 234 139 131 |
| Edge42 (Tokio) | `mboxedge42.tt.omtrdc.net` | 52 194 84 34<br />3 115 158 39 <br />18 180 123 21 |
| Edge44 (Ostküste USA) | `mboxedge44.tt.omtrdc.net` | 54 205 210 54<br />23,20,189,8 <br />35 169 173 155 |
| Edge45 (Westküste USA) | `mboxedge45.tt.omtrdc.net` | 35 161 163 45<br />44 230 114 101 <br />35 161 120 22 |
| Edge46 (Sydney) | `mboxedge46.tt.omtrdc.net` | 3 104 142 61<br />52 62 4 152 <br />54 253 105 140 |
| Edge47 (Irland) | `mboxedge47.tt.omtrdc.net` | 18 203 168 186<br />54 228 83 91 <br />54 217 181 83 |
| Edge48 (Singapur) | `mboxedge48.tt.omtrdc.net` | 54 179 6 70<br />13 215 150 94 <br />18 136 47 70 |

Da die Lastenausgleichsmodule Änderungen im Traffic-Profil erkennen, wird es nach oben oder unten skaliert. Die für den Elastic Load Balancing erforderliche Zeit kann je nach erkannten Änderungen zwischen 1 und 7 Minuten betragen. Wenn der Lastenausgleich skaliert wird, aktualisiert er den DNS-Eintrag mit der neuen Liste der IP-Adressen. Um sicherzustellen, dass Sie die erhöhte Kapazität nutzen, verwendet der Elastic Load Balancing eine TTL-Einstellung für den DNS-Eintrag von 60 Sekunden.
