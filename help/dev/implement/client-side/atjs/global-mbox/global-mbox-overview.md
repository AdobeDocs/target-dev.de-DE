---
keywords: Globale Mbox, Implementierung von at.js
description: Erfahren Sie mehr über die globale Mbox in [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] Implementierung.
title: Was ist eine globale Mbox?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 61%

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
