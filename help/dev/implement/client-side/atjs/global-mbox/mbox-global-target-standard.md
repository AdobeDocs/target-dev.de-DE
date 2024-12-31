---
keywords: globale mbox, Target Classic, globale Mbox mit Target Classic verwenden
description: Erfahren Sie, wie Sie eine ältere globale Mbox für Ihre - [!DNL Adobe Target]  verwenden, wenn Sie bereits eine globale Mbox auf Ihren Seiten für Ihre Legacy-Implementierungen erstellt haben.
title: Kann ich eine globale Mbox in einer Legacy-Implementierung verwenden?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
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
