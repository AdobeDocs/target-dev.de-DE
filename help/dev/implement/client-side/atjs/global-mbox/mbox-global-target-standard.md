---
keywords: globale mbox, Target Classic, globale Mbox mit Target Classic verwenden
description: Erfahren Sie, wie Sie eine ältere globale Mbox für Ihre [!DNL Adobe Target] Aktivitäten , wenn Sie bereits eine globale Mbox für Ihre älteren Implementierungen auf Ihren Seiten erstellt haben.
title: Kann ich eine globale Mbox aus einer älteren Implementierung verwenden?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 39%

---

# Verwenden einer globalen Mbox aus einer älteren Implementierung

Standardmäßig ist [!DNL Target] erstellt eine globale Mbox mit der Bezeichnung target-global-mbox , die zum Ausführen von Aktivitäten verwendet wird, die in erstellt wurden. [!DNL Target]. Wenn Sie auf Ihren Seiten jedoch bereits eine globale MBox für Ihre bestehende Implementierung erstellt haben, können Sie diese MBox für Ihre [!DNL Target]-Aktivitäten verwenden.

>[!NOTE]
>
>Es ist nur eine globale Mbox pro Konto zulässig.

Sie müssen einige Parameter festlegen, um Ihre vorhandene globale MBox für [!DNL Target] und Ihre bestehende Implementierung verwenden zu können.

1. Navigieren Sie zu [!DNL Target]Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.

   Standardmäßig ist **[!UICONTROL Seitenladeaktivierung (globale Mbox automatisch erstellen]** aktiviert ist und die benutzerdefinierte globale Mbox `target-global-mbox`.

1. Wenn Sie eine vorhandene Mbox verwenden möchten, deaktivieren Sie **[!UICONTROL Seitenladeaktivierung (globale Mbox automatisch erstellen]** und geben Sie den Namen einer zuvor erstellten globalen Mbox im **[!UICONTROL Globale Mbox]** -Feld.

   In der Dropdownliste Globale Mbox werden alle Mboxes in Ihrem Konto aufgelistet. Wenn Sie eine Mbox verwenden möchten, die noch nicht vorhanden ist, erstellen Sie diese.

1. Klicken Sie auf **[!UICONTROL Speichern]**.

   Die Einstellungen für Ihr Konto werden aktualisiert.

1. Laden Sie die neue at.js-Datei herunter und referenzieren Sie sie auf Ihrer Site.

   Alle bestehenden Aktivitäten werden aktualisiert, sodass diese die angegebene globale Mbox verwenden, einschließlich zuvor erstellter und implementierter Aktivitäten.

## Fehlerbehebung bei der Implementierung der globalen Mbox

Die folgenden häufig gestellten Fragen können zur Fehlerbehebung bei Ihrer globalen Mbox-Implementierung verwendet werden:

### Wieso wird die globale Mbox nicht geladen oder wieso gibt es eine Wartezeit beim Laden der globalen Mbox beim Laden der Seite?

Stellen Sie sicher, dass die at.js-Referenz der erste JavaScript-Aufruf auf der Seite ist. Weitere Lösungen für dieses Problem finden Sie unter [Häufig gestellte Fragen zu globalen Mboxes](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md).
