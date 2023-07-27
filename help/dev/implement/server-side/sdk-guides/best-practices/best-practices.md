---
title: Best Practices bei der Verwendung von Entscheidungen auf dem Gerät
description: Best Practices bei der Verwendung von [!UICONTROL on-device decisioning] in [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# Best Practices

[!DNL Adobe] empfiehlt die folgenden Best Practices für die Verwendung von [!UICONTROL on-device decisioning]:

## Best Practices bei der Entscheidungsmethode &quot;on device&quot;

Bei Verwendung von &quot;on-device&quot;als Entscheidungsmethode wird das Artefakt heruntergeladen, wenn der Besucher die Webseite zum ersten Mal lädt. Eine Aktivitätsqualifikation, die beim ersten Laden der Seite (kein Cache) durchgeführt werden muss, erfolgt erst, nachdem das Artefakt vollständig heruntergeladen wurde. Es gibt bestimmte Best Practices, die Sie anwenden können, um sicherzustellen, dass Aktivitätsqualifikationen für einen neuen anonymen Besucher schnell erfolgen.

* Deaktivieren Sie &quot;On-Device&quot;-fähige Aktivitäten, die nicht im Artefakt enthalten sein sollen.
* Wenn Sie über Target Premium verfügen, können Sie [Eigenschaften/Arbeitsbereiche](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=de) , um verschiedene Artefaktdateien für verschiedene Arbeitsbereiche zu erstellen.
* Wenn Ihre Artefaktdateien aus berechtigten Gründen sehr groß werden, können Sie die &quot;hybride&quot;Entscheidungsmethode verwenden. Mit dieser Methode können Sie das Artefakt parallel herunterladen. Alle Target-API-Aufrufe werden so lange über das Kabel gesendet, bis das Artefakt heruntergeladen wurde. Weitere Informationen zu diesem Ansatz finden Sie im Abschnitt zu Best Practices im Hybrid-Entscheidungsmodus unten.
* Wenn Sie über eine Einzelseiten-App verfügen (SPA), [!DNL Adobe] empfiehlt, at.js zu laden und zu initialisieren, bevor Sie beim ersten Laden der Seite die JavaScript-Hauptdatei Ihrer Anwendung laden. Dieser Ansatz startet das Herunterladen des Artefakts viel früher und ermöglicht so ein schnelleres Erlebnis-Rendering.

## Best Practices bei der Entscheidungsmethode &quot;hybrid&quot;

Bei Verwendung von &quot;hybrid&quot;als Entscheidungsmethode wird das Artefakt parallel heruntergeladen. Bis zum Herunterladen des Artefakts können alle [!DNL Target] API-Aufrufe gehen über das Netzwerk, selbst wenn die &quot;Standorte&quot;gerätefähig sind. Dieses Verhalten ist standardmäßig für alle `getOffers()` und bietet in den meisten Situationen die beste Leistung. Wenn Sie das Standardverhalten von `getOffers()` durch Festlegen der `decisioningMethod` nach `on-device`folgen Sie diesen Best Practices, um Fehler zu vermeiden und die beste Leistung sicherzustellen.

* Wenn Sie sich entscheiden, `getOffers()` mit `decisioningMethod` as `on-device` Wenn die Seite zum ersten Mal geladen wird, müssen Sie dies im at.js-Ereignishandler &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot;tun, um Fehler zu vermeiden. Wenn Ihr Artefakt sehr groß ist, werden alle &quot;Orte&quot;, die diesen Ansatz verwenden, erst gerendert, nachdem das Artefakt vollständig heruntergeladen wurde. Dies kann das Rendern von Erlebnissen verzögern. [!DNL Adobe] empfiehlt, diesen Ansatz selten zu verwenden. Befolgen Sie bei Verwendung dieses Ansatzes die Best Practices zur Reduzierung der Artefaktgröße im Abschnitt &quot;Best Practices auf dem Gerät&quot;.
