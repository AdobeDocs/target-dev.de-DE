---
keywords: Globale Mbox, Implementierung von at.js
description: Erfahren Sie mehr über die globale Mbox in [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] Implementierung.
title: Was ist eine globale Mbox?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 62%

---

# Erläuterung der globalen Mbox

Informationen über die globale Mbox, ein Name, der auf den einzelnen Server-Aufruf verweist, der oben auf jeder Web-Seite in Ihrer [!DNL Adobe Target]-Implementierung erfolgt.

Standardmäßig erhält die globale Mbox den Namen `target-global-mbox`. Sie kann für Ihr Konto bei Bedarf aber auch umbenannt werden.

Es gibt einige Unterschiede zwischen einer normalen Mbox (nicht globale Mbox) und der globalen Mbox, darunter die folgenden:

| Normale Mbox | Globale Mbox |
|--- |--- |
| Eine normale Mbox bricht um Inhalte normalerweise mit dem Tag `<DIV>` um. | Die globale Mbox ist „leer“ und bricht nicht um Inhalt um. |
| In einer normalen Mbox kann nur Inhalt einer Aktivität bereitgestellt werden. | In einer Antwort an eine globale Mbox können Inhalte mehrerer Aktivitäten bereitgestellt werden. |

Werden mehrere Aktivitäten über die globale Mbox oder mehrere reguläre Mboxes bereitgestellt, bestimmt Target [die Priorität), mit ](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) die Aktivität (oder Aktivitäten) auf einer Web-Seite bereitgestellt wird.

Es lassen sich zusätzliche Daten auf Seitenniveau an [!DNL Target] sowie an die globale Mbox übermitteln, indem die Funktion `[!UICONTROL targetPageParams]` genutzt wird. Dies entspricht in etwa der Funktion für Mbox-Parameter. Weitere Informationen finden Sie unter [Übergeben von Parametern an eine globale Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md).
