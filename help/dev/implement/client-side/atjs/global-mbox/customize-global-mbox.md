---
keywords: globale Mbox, globale Mbox anpassen, at.js bearbeiten, at.js, at.js implementieren
description: Erfahren Sie, wie Sie eine globale Mbox für at.js auf der Seite [!UICONTROL Administration]-[!UICONTROL Implementierung] Seite in [!DNL Adobe Target].
title: Wie kann ich eine globale Mbox anpassen?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# Anpassen einer globalen Mbox

Informationen, die Sie bei der Anpassung eines [!DNL Adobe Target] globale Mbox für at.js.

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]**.

1. Deaktivieren **[!UICONTROL Seitenladung aktiviert (globale Mbox automatisch erstellen)]** und fügen Sie dann den Namen der benutzerdefinierten globalen Mbox hinzu, die Sie verwenden möchten, um Aktivitäten aus bereitzustellen. [!DNL Target].

>[!WARNING]
>
>Die Änderung wird automatisch gespeichert, wenn Sie eine andere globale Mbox auswählen.

Die globale Mbox wird auch für Klick-Tracking eingesetzt.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implementieren Sie die at.js-Bibliothek auf Ihrer Site.

   Siehe [Implementieren von &quot;at.js&quot;](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) für weitere Informationen.

1. Stimmen Sie die Umstellung mit Ihrer Veröffentlichung zeitlich ab.

   Wenn Sie bereit sind für [!DNL Target] um in Zukunft Ihre globale Mbox für alle Aktivitäten zu verwenden, können Sie mit diesem Schritt fortfahren.

   Aktualisieren Sie den Namen der globalen mbox, sodass er dem in Schritt 2 (siehe oben) verwendeten Namen entspricht.


>[!WARNING]
>
>Alle Aktivitäten in Ihrem Konto werden mit dieser Mbox synchronisiert. Stellen Sie sicher, dass die globale Mbox auf Ihrer Site vorhanden ist, damit die Aktivitäten weiterhin funktionieren. Achten Sie darauf, die betroffenen Aktivitäten, die mit der [!UICONTROL Visual Experience Composer] (VEC), die mit dieser Mbox synchronisiert werden. Es ist nicht erforderlich, die in der Variablen [!UICONTROL Form-Based Experience Composer] oder über API.
