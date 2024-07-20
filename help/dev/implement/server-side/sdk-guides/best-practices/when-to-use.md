---
source-git-commit: 5c66ee5c8dd5fe60eaeed10fdb9bb6dcee000c89
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---
# Verwendung von geräteübergreifenden gegenüber Edge-Entscheidungen

## Berücksichtigen Sie Anwendungsfälle bei der Entscheidung, ob Sie Entscheidungen auf dem Gerät treffen sollten.

![alt image](assets/comparison.jpeg)

Der Hauptunterschied zwischen der Entscheidung für *auf dem Gerät* und der Edge-Entscheidung besteht darin, dass Entscheidungen auf dem Gerät lokal auf Ihren Servern ausgeführt werden, während Edge-Entscheidungen auf dem Edge-Netzwerk von Adobe Target getroffen werden. Die Entscheidungsfindung auf dem Gerät sollte für alle A/B- oder XT-Aktivitäten verwendet werden, die auf Seiten mit hohem Traffic bereitgestellt werden müssen, auf denen die Leistung erhebliche Auswirkungen auf Ihre geschäftlichen KPIs wie Konversion, Umsatz und Bindung hat. Angenommen, Ihr Marketing-Team führt Werbekampagnen durch, um Interessenten für Ihre Homepage zu gewinnen. Die Durchführung von Werbekampagnen in Publisher-Netzwerken erfordert eine Zahlung, daher wird jede Aussicht, die auf Ihre Homepage gelangt, auf einen Dollarbetrag umgerechnet. Angenommen, Sie führen A/B-Experimente durch, um zu sehen, welches Hero-Bild die Aufmerksamkeit Ihres Verbrauchers am besten erfasst. Wenn die Bereitstellung dieser A/B-Experimente zusätzliche 2 Sekunden in Anspruch nimmt, besteht eine hohe Wahrscheinlichkeit, dass der Verbraucher ungeduldig wird und Bounces erhält. Es gibt Ihre Marketing-Dollars und A/B-Experimente! Der Verlust dieser hart verdienten Perspektive ist schwierig, da jede Möglichkeit, diese Perspektive in einen treuen oder wiederkehrenden Kunden umzuwandeln, nun verwirkt wird. Die Ausführung einer Entscheidungsaktivität auf dem Gerät für diesen Anwendungsfall kann daher negative Auswirkungen vermeiden, die Latenzzeiten verursachen können.

Andererseits erfordert die Edge-Entscheidungsfindung einen Netzwerkblockieraufruf, um ein Erlebnis abzurufen. Dies kann jedoch äußerst vorteilhaft sein, da Echtzeitdaten und ML verwendet werden können, um das Endbenutzererlebnis äußerst ansprechend zu gestalten. Ein Netzwerkblockieraufruf führt zu einer zusätzlichen Latenz bei der Bereitstellung des Erlebnisses. In einigen Szenarien kann dieser Kompromiss jedoch sinnvoll sein. Betrachten Sie beispielsweise ein Szenario, in dem ein Kunde durch Ihren Produktkatalog navigiert, und nehmen Sie an, dass er zu einer Produktdetailseite navigiert. Wenn auf dieser Seite eine empfohlene Liste von Produkten zusammen mit dem Produkt angezeigt wird, das der Kunde derzeit anzeigt, kann dies die Interaktion - und später die Konversion und den Umsatz steigern. Die Anzeige der empfohlenen Produktliste auf diese Weise würde zwar eine vom ML-Algorithmus von Adobe Target beeinflusste Edge-Entscheidung erfordern - d. h., es würde eine zusätzliche Latenz hinzugefügt -, doch wäre die hinzugefügte Latenz nicht bedeutend genug, damit der Endbenutzer Bounce starten kann. Darüber hinaus führt eine empfohlene Produktliste zu einer höheren Konversionsrate. Daher bietet eine Edge-Entscheidung in diesem Fall Ihrem Unternehmen den größten Wert.

## Unterstützte Funktionen

Überprüfen Sie neben der Bewertung Ihrer Anwendungsfälle und Geschäftsziele, welche Funktionen die On-Device-Entscheidungsfindung [unterstützt](../on-device-decisioning/supported-features.md), bevor Sie entscheiden, ob Sie die On-Device-Entscheidungsfindung und die Edge-Entscheidungsfindung verwenden möchten. Derzeit unterstützt Edge Decisioning alle Aktivitätstypen, Zielgruppen-Targeting und Zuordnungsmethoden.