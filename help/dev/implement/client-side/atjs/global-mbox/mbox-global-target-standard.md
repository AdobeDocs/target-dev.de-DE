---
keywords: globale mbox, Target Classic, globale Mbox mit Target Classic verwenden
description: Erfahren Sie, wie Sie eine ältere globale Mbox für Ihre - [!DNL Adobe Target]  verwenden, wenn Sie bereits eine globale Mbox auf Ihren Seiten für Ihre Legacy-Implementierungen erstellt haben.
title: Kann ich eine globale Mbox in einer Legacy-Implementierung verwenden?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 285
ht-degree: 20%

---

# Verwenden einer globalen Mbox in einer Legacy-Implementierung

Standardmäßig erstellt [!DNL Target] eine globale Mbox mit dem Namen target-global-mbox, die zum Ausführen von in [!DNL Target] erstellten Aktivitäten verwendet wird. Wenn Sie jedoch bereits eine globale Mbox auf Ihren Seiten für Ihre Legacy-Implementierungen erstellt haben, können Sie diese Mbox für Ihre [!DNL Target]-Aktivitäten verwenden.

>[!NOTE]
>
>Es ist nur eine globale Mbox pro Konto zulässig.

Sie müssen einige Parameter festlegen, um Ihre vorhandene globale MBox für [!DNL Target] und Ihre bestehende Implementierung verwenden zu können.

1. Gehen Sie zu [!DNL Target] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   Standardmäßig ist **[!UICONTROL Page load enabled (Auto-create global mbox]** aktiviert und die benutzerdefinierte globale Mbox trägt den Namen `target-global-mbox`.

1. Wenn Sie eine vorhandene Mbox verwenden möchten, deaktivieren Sie **[!UICONTROL Page load enabled (Auto-create global mbox]**, und geben Sie den Namen einer zuvor erstellten globalen Mbox im Feld **[!UICONTROL Global Mbox]** an.

   In der Dropdown-Liste Globale Mbox werden alle Mboxes in Ihrem Konto aufgelistet. Wenn Sie eine Mbox verwenden möchten, die noch nicht vorhanden ist, erstellen Sie die Mbox.

1. Klicken Sie auf **[!UICONTROL Save]**.

   Die Einstellungen für Ihr Konto werden aktualisiert.

1. Laden Sie die neue Datei „at.js“ herunter und verweisen Sie auf Ihrer Site darauf.

   Alle bestehenden Aktivitäten werden aktualisiert, sodass diese die angegebene globale Mbox verwenden, einschließlich zuvor erstellter und implementierter Aktivitäten.

## Fehlerbehebung bei der Implementierung der globalen Mbox

Die folgenden häufig gestellten Fragen können zur Fehlerbehebung bei der Implementierung Ihrer globalen Mbox verwendet werden:

### Warum wird die globale Mbox nicht geladen, oder warum kommt es beim Laden der globalen Mbox beim Laden der Seite zu einer Latenz?

Stellen Sie sicher, dass die at.js-Referenz der erste JavaScript-Aufruf auf der Seite ist. Weitere Lösungen für dieses Problem finden Sie unter [Häufig gestellte Fragen zu globalen Mboxes](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
