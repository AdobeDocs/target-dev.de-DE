---
source-git-commit: 5c66ee5c8dd5fe60eaeed10fdb9bb6dcee000c89
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---
# Wann die geräteinterne vs. die Edge-Entscheidungsfindung verwendet werden sollte

## Berücksichtigen Sie Anwendungsfälle, wenn Sie entscheiden, ob die geräteinterne Entscheidungsfindung verwendet werden soll

![ALT-Bild](assets/comparison.jpeg)

Der Hauptunterschied zwischen *On-Device Decisioning* und Edge Decisioning besteht darin, dass Entscheidungen auf dem Gerät lokal auf Ihren Servern ausgeführt werden, während Edge-Entscheidungen auf dem Edge-Netzwerk von Adobe Target getroffen werden. Die geräteinterne Entscheidungsfindung sollte für alle A/B- oder XT-Aktivitäten verwendet werden, die auf Seiten mit hohem Traffic bereitgestellt werden müssen, wobei sich die Leistung stark auf Ihre geschäftlichen KPIs wie Konversion, Umsatz und Kundenbindung auswirkt. Angenommen, Ihr Marketing-Team führt Werbekampagnen aus, um Interessenten für Ihre Homepage zu gewinnen. Das Ausführen von Werbekampagnen in Publisher-Netzwerken erfordert eine Zahlung. Daher wird jeder potenzielle Kunde, der auf Ihrer Homepage landet, in einen Dollar-Betrag umgewandelt. Angenommen, Sie führen A/B-Experimente durch, um zu sehen, welches Hero-Bild die Aufmerksamkeit Ihrer Kunden am besten auf sich zieht. Wenn die Bereitstellung dieser A/B-Experimente weitere 2 Sekunden dauert, ist die Wahrscheinlichkeit hoch, dass der Verbraucher ungeduldig wird und abspringt. Da haben Sie Ihr Marketing-Geld und A/B-Experimente! Dieser hart erarbeitete potenzielle Kunde kann nur schwer verloren gehen, da jede Möglichkeit, diesen potenziellen Kunden in einen treuen oder wiederkehrenden Kunden umzuwandeln, jetzt vertan wird. Daher kann die Ausführung einer Entscheidungsaktivität auf dem Gerät für diesen Anwendungsfall jede negative Auswirkung vermeiden, die durch Latenz entstehen kann.

Andererseits erfordert Edge Decisioning einen Netzwerkblockieraufruf, um ein Erlebnis abzurufen. Dies kann jedoch sehr vorteilhaft sein, da Echtzeitdaten und ML verwendet werden können, um das Endbenutzererlebnis sehr ansprechend zu gestalten. Ein Netzwerk-Blockierungsaufruf führt zu einer zusätzlichen Latenz bei der Bereitstellung des Erlebnisses. In einigen Szenarien kann dieser Kompromiss jedoch sinnvoll sein. Angenommen, ein Kunde durchsucht Ihren Produktkatalog und navigiert zu einer Produktdetailseite. Wenn auf dieser Seite eine empfohlene Liste von Produkten zusammen mit dem Produkt angezeigt wird, das der Kunde derzeit anzeigt, kann dies die Interaktion und später die Konversionen und Umsätze steigern. Wenn Sie die empfohlene Produktliste auf diese Weise anzeigen, wäre eine Edge-Entscheidung erforderlich, die durch den ML-Algorithmus von Adobe Target beeinflusst wird - was bedeutet, dass es eine zusätzliche Latenz geben würde -, dass die zusätzliche Latenz nicht signifikant genug ist, damit der Endbenutzer abspringen kann. Darüber hinaus führt eine empfohlene Produktliste zu einer höheren Konversionsrate. Daher bietet in diesem Fall eine Edge-Entscheidung Ihrem Unternehmen den größten Nutzen.

## Unterstützte Funktionen

Überprüfen Sie nicht nur Ihre Anwendungsfälle und Geschäftsziele, sondern auch, welche Funktionen die geräteinterne Entscheidungsfindung [unterstützt](../on-device-decisioning/supported-features.md) bevor Sie entscheiden, ob die geräteinterne Entscheidungsfindung im Vergleich zur Edge-Entscheidungsfindung verwendet werden soll. Derzeit unterstützt Edge Decisioning alle Aktivitätstypen, Zielgruppen-Targeting und Zuordnungsmethoden.