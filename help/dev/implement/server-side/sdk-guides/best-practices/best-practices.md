---
title: Best Practices bei der Verwendung der geräteinternen Entscheidungsfindung
description: Erfahren Sie mehr über Best Practices bei der Verwendung von [!UICONTROL on-device decisioning] in  [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Best Practices

[!DNL Adobe] empfiehlt die folgenden Best Practices bei der Verwendung von [!UICONTROL on-device decisioning]:

## Best Practices, wenn die Entscheidungsmethode auf dem Gerät ausgeführt wird

Bei Verwendung von „auf dem Gerät“ als Entscheidungsmethode wird das Artefakt heruntergeladen, wenn der Besucher die Web-Seite zum ersten Mal lädt. Jede Aktivitätsqualifizierung, die beim ersten Laden der Seite erfolgen muss (kein Cache), erfolgt erst, nachdem das Artefakt vollständig heruntergeladen wurde. Es gibt bestimmte Best Practices, die Sie befolgen können, um sicherzustellen, dass Aktivitätsqualifikationen für einen neuen anonymen Besucher schnell passieren.

* Deaktivieren Sie „On-Device“-fähige Aktivitäten, die nicht im Artefakt enthalten sein sollen.
* Wenn Sie über Target Premium verfügen, können Sie [properties/workspaces](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de) verwenden, um verschiedene Artefaktdateien für verschiedene Arbeitsbereiche zu erstellen.
* Wenn Ihre Artefaktdateien aus legitimen Gründen sehr groß werden, können Sie die „hybride“ Entscheidungsmethode verwenden. Mit dieser Methode können Sie das Artefakt parallel herunterladen, und alle Target-API-Aufrufe gehen über die Verbindung, bis das Artefakt heruntergeladen wurde. Lesen Sie den Abschnitt Best Practices für den „hybriden“ Entscheidungsmodus unten, um mehr über diesen Ansatz zu erfahren.
* Wenn Sie über eine Einzelseiten-App (SPA) verfügen, empfiehlt [!DNL Adobe], at.js zu laden und zu initialisieren, bevor Sie beim ersten Laden der Seite die JavaScript-Hauptdatei Ihrer Anwendung laden. Durch diesen Ansatz wird der Download des Artefakts viel früher gestartet, was ein schnelleres Rendern des Erlebnisses ermöglicht.

## Best Practices, wenn die Entscheidungsmethode „hybrid“ ist

Bei Verwendung von „Hybrid“ als Entscheidungsmethode wird das Artefakt parallel heruntergeladen. Bis das Artefakt heruntergeladen wird, werden alle [!DNL Target]-API-Aufrufe über die Verbindung gesendet, selbst wenn die „Standorte“ auf dem Gerät verfügbar sind. Dieses Verhalten ist die Standardeinstellung für alle `getOffers()`-Aufrufe und bietet in den meisten Situationen die beste Leistung. Wenn Sie das Standardverhalten von `getOffers()` ändern, indem Sie die `decisioningMethod` auf `on-device` setzen, befolgen Sie die folgenden Best Practices, um Fehler zu vermeiden und die beste Leistung sicherzustellen.

* Wenn Sie sich entscheiden, `getOffers()` beim ersten Laden der Seite mit `decisioningMethod` als `on-device` aufzurufen, müssen Sie dies innerhalb des „ARTIFACT_DOWNLOAD_SUCCEEDED“ at.js-Ereignis-Handlers tun, um Fehler zu vermeiden. Wenn Ihr Artefakt sehr groß ist, werden alle „Speicherorte“, die diesen Ansatz verwenden, erst gerendert, nachdem das Artefakt vollständig heruntergeladen wurde, was das Erlebnis-Rendering verzögern kann. [!DNL Adobe] empfiehlt, diesen Ansatz nur selten zu verwenden. Befolgen Sie bei diesem Ansatz die Best Practices zur Reduzierung der Artefaktgröße im obigen Abschnitt „Best Practices auf dem Gerät“.
