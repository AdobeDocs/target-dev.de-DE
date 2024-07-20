---
keywords: globale mbox, Target Classic, globale Mbox mit Target Classic verwenden
description: Erfahren Sie, wie Sie eine ältere globale Mbox für Ihre [!DNL Adobe Target] Aktivitäten verwenden können, wenn Sie bereits eine globale Mbox für Ihre älteren Implementierungen auf Ihren Seiten erstellt haben.
title: Kann ich eine globale Mbox aus einer älteren Implementierung verwenden?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 20%

---

# Verwenden einer globalen Mbox aus einer älteren Implementierung

Standardmäßig erstellt [!DNL Target] eine globale Mbox mit der Bezeichnung target-global-mbox, die zum Ausführen von in [!DNL Target] erstellten Aktivitäten verwendet wird. Wenn Sie jedoch bereits eine globale Mbox für Ihre älteren Implementierungen auf Ihren Seiten erstellt haben, können Sie diese Mbox für Ihre [!DNL Target] -Aktivitäten verwenden.

>[!NOTE]
>
>Es ist nur eine globale Mbox pro Konto zulässig.

Sie müssen einige Parameter festlegen, um Ihre vorhandene globale MBox für [!DNL Target] und Ihre bestehende Implementierung verwenden zu können.

1. Gehen Sie zu [!DNL Target] und klicken Sie dann auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

   Standardmäßig ist **[!UICONTROL Page load enabled (Auto-create global mbox]** aktiviert und die benutzerdefinierte globale Mbox heißt `target-global-mbox`.

1. Wenn Sie eine vorhandene Mbox verwenden möchten, deaktivieren Sie **[!UICONTROL Page load enabled (Auto-create global mbox]** und geben Sie den Namen einer zuvor erstellten globalen Mbox im Feld **[!UICONTROL Global Mbox]** an.

   In der Dropdownliste Globale Mbox werden alle Mboxes in Ihrem Konto aufgelistet. Wenn Sie eine noch nicht vorhandene Mbox verwenden möchten, erstellen Sie die Mbox.

1. Klicken Sie auf **[!UICONTROL Save]**.

   Die Einstellungen für Ihr Konto werden aktualisiert.

1. Laden Sie die neue at.js-Datei herunter und referenzieren Sie sie auf Ihrer Site.

   Alle bestehenden Aktivitäten werden aktualisiert, sodass diese die angegebene globale Mbox verwenden, einschließlich zuvor erstellter und implementierter Aktivitäten.

## Fehlerbehebung bei der Implementierung der globalen Mbox

Die folgenden häufig gestellten Fragen können zur Fehlerbehebung bei Ihrer globalen Mbox-Implementierung verwendet werden:

### Warum wird die globale Mbox nicht geladen oder wieso gibt es eine Wartezeit beim Laden der globalen Mbox beim Laden der Seite?

Stellen Sie sicher, dass der at.js-Verweis der erste JavaScript-Aufruf auf der Seite ist. Weitere Lösungen zu diesem Problem finden Sie unter [Häufig gestellte Fragen zu globalen Mboxes](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
