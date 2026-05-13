---
keywords: Globale Mbox, Globale Mbox anpassen, at.js bearbeiten, at.js implementieren, at.js
description: Erfahren Sie, wie Sie auf der Seite "[!UICONTROL Administration]-[!UICONTROL Implementation]" in eine globale Mbox für at.js  [!DNL Adobe Target].
title: Wie kann ich eine globale Mbox anpassen?
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
TQID: https://experienceleague.adobe.com/MtbjwpKrZ-WmBnE5tBY74oJgQVB-zPLrCuFDrFshkGo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 18%

---

# Anpassen einer globalen Mbox

Informationen zum Anpassen einer [!DNL Adobe Target] globalen Mbox für at.js.

1. Klicken Sie auf **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**.

1. Deaktivieren Sie **[!UICONTROL Page load enabled (Auto create global mbox)]** und fügen Sie dann den Namen der benutzerdefinierten globalen Mbox hinzu, die Sie zum Bereitstellen von Aktivitäten aus [!DNL Target] verwenden möchten.

>[!WARNING]
>
>Die Änderung wird automatisch gespeichert, wenn Sie eine andere globale Mbox auswählen.

Die globale Mbox wird auch für Klick-Tracking eingesetzt.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. Implementieren Sie die at.js-Bibliothek auf Ihrer Site.

   Weitere Informationen finden [ unter „Bereitstellen von ](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md).js“ .

1. Stimmen Sie die Umstellung mit Ihrer Veröffentlichung zeitlich ab.

   Wenn Sie bereit sind, [!DNL Target] Ihre globale Mbox für alle zukünftigen Aktivitäten zu verwenden, können Sie mit diesem Schritt fortfahren.

   Aktualisieren Sie den Namen der globalen mbox, sodass er dem in Schritt 2 (siehe oben) verwendeten Namen entspricht.


>[!WARNING]
>
>Alle Aktivitäten in Ihrem Konto werden mit dieser Mbox synchronisiert. Stellen Sie sicher, dass die globale Mbox auf Ihrer Site vorhanden ist, damit die Aktivitäten weiterhin funktionieren. Achten Sie darauf, die betroffenen Aktivitäten zu bearbeiten und erneut zu speichern, die mit dem [!UICONTROL Visual Experience Composer] (VEC) erstellt wurden, der mit dieser Mbox synchronisiert wird. Es ist nicht erforderlich, in der [!UICONTROL Form-Based Experience Composer] oder über die API erstellte Aktivitäten erneut zu speichern.
