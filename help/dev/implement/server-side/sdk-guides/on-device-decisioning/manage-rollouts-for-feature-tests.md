---
title: Verwalten von Rollouts für Funktionstests
description: Erfahren Sie, wie Sie Rollouts für Funktionstests mit [!UICONTROL on-device decisioning].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Verwalten von Rollouts für Funktionstests

## Zusammenfassung der Schritte

1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation
1. Erstellen Sie eine [!UICONTROL A/B-Test] activity
1. Definieren Sie Ihre Funktionen und Rollout-Einstellungen
1. Funktion in Ihre Anwendung implementieren und rendern
1. Implementieren des Trackings für Ereignisse in Ihrer Anwendung
1. A/B-Aktivität aktivieren
1. Passen Sie die Rollout- und Traffic-Zuordnung nach Bedarf an

## 1. Aktivieren [!UICONTROL on-device decisioning] für Ihre Organisation

Durch die Aktivierung der Entscheidungsfindung auf dem Gerät wird sichergestellt, dass eine A/B-Aktivität mit nahezu Nulllatenz ausgeführt wird. Navigieren Sie zur Aktivierung dieser Funktion zu **[!UICONTROL Administration]** > **[!UICONTROL Implementierung]** > **[!UICONTROL Kontodetails]** in [!DNL Adobe Target]und aktivieren Sie die **[!UICONTROL On-Device Decisioning]** umschalten.

![ALT-Bild](assets/asset-odd-toggle.png)

>[!NOTE]
>
>Sie müssen über einen Administrator oder Genehmiger verfügen. [Benutzerrolle](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) , um die [!UICONTROL On-Device Decisioning] umschalten.

Nach der Aktivierung der [!UICONTROL On-Device Decisioning] Umschalten, [!DNL Adobe Target] beginnt zu generieren *ruleArtefakte* für Ihren Client.

## 2. Erstellen Sie eine [!UICONTROL A/B-Test] activity

1. In [!DNL Adobe Target], navigieren Sie zum **[!UICONTROL Tätigkeiten]** Seite und wählen Sie **[!UICONTROL Aktivität erstellen]** > **[!UICONTROL A/B-Test]**.

   ![ALT-Bild](assets/asset-ab.png)

1. Im **[!UICONTROL A/B-Test-Aktivität erstellen]** modal, Behalten Sie die Standardeinstellung bei **[!UICONTROL Web]** ausgewählte Option (1), wählen Sie **[!UICONTROL Formular]** Wählen Sie als Experience Composer (2) **[!UICONTROL Standardarbeitsbereich]** mit **[!UICONTROL Keine Eigenschaftenbeschränkungen]** (3) und klicken Sie auf **[!UICONTROL Nächste]** 4.

   ![ALT-Bild](assets/asset-form.png)

## 3. Definieren Sie Ihre Funktionen und Rollout-Einstellungen.

Im **[!UICONTROL Erlebnisse]** Schritt der Aktivitätserstellung einen Namen für Ihre Aktivität angeben (1). Geben Sie den Namen des Speicherorts (2) in Ihrer Anwendung ein, in dem Sie Rollouts für Ihre Funktion verwalten möchten. Beispiel:  `ondevice-rollout` oder `homepage-addtocart-rollout` sind Ortsnamen, die die Ziele für die Verwaltung von Funktions-Rollouts angeben. Im folgenden Beispiel: `ondevice-rollout` ist der für Erlebnis A definierte Ort. Sie können optional Zielgruppenverfeinerungen (4) hinzufügen, um die Qualifizierung auf die Aktivität zu beschränken.

![ALT-Bild](assets/asset-location-rollout.png)

1. Im **[!UICONTROL Inhalt]** auf derselben Seite ein und wählen Sie **[!UICONTROL JSON-Angebot erstellen]** in der Dropdown-Liste (1) angezeigt.

   ![ALT-Bild](assets/asset-offer.png)

1. Im **[!UICONTROL JSON-Daten]** eingeben, die Variable für die Feature Flag für die Funktion eingeben, die Sie mit dieser Aktivität in Erlebnis A (1) mit einem gültigen JSON-Objekt (2) einführen möchten.

   ![ALT-Bild](assets/asset-json-a-rollout.png)

1. Klicks **[!UICONTROL Nächste]** 1. **[!UICONTROL Targeting]** Schritt der Aktivitätserstellung.

   ![ALT-Bild](assets/asset-next-2-t-rollout.png)

1. Im **[!UICONTROL Targeting]** halten Sie die **[!UICONTROL Alle Besucher]** Zielgruppe (1) aus Gründen der Einfachheit. Die Traffic-Zuordnung (2) sollte jedoch auf 10 % angepasst werden. Dadurch wird die Funktion auf nur 10 % der Site-Besucher beschränkt. Klicken Sie auf Weiter (3) , um zum **[!UICONTROL Ziele und Einstellungen]** Schritt.

   ![ALT-Bild](assets/asset-next-2-g-rollout.png)

1. Im **[!UICONTROL Ziele und Einstellungen]** Schritt auswählen **[!UICONTROL Adobe Target]** 1. als **[!UICONTROL Berichtsquelle]** um Ihre Aktivitätsergebnisse im [!DNL Adobe Target] Benutzeroberfläche.

1. Wählen Sie eine **[!UICONTROL Zielmetrik]** , um die Aktivität zu messen. In diesem Beispiel basiert eine erfolgreiche Konvertierung darauf, ob der Benutzer einen Artikel kauft, was daran erkennbar ist, ob der Benutzer den Speicherort orderConfirm (2) erreicht hat.

1. Klicks **[!UICONTROL Speichern und schließen]** (3) , um die Aktivität zu speichern.

   ![ALT-Bild](assets/asset-conv-rollout.png)

## 4. Implementieren und Rendern der Funktion in Ihrer Anwendung

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java ]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## 5. Implementieren des Trackings für Ereignisse in Ihrer Anwendung

Nachdem Sie die Variable &quot;Feature Flag&quot;in der Anwendung verfügbar gemacht haben, können Sie sie verwenden und alle Funktionen aktivieren, die bereits Teil Ihrer Anwendung sind. Wenn ein Besucher nicht für die Aktivität qualifiziert ist, bedeutet dies, dass er nicht Teil der 10-%-Gruppe war, die als Zielgruppe definiert wurde.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java ]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## 6. Aktivieren Sie Ihre Rollout-Aktivität

![ALT-Bild](assets/asset-activate-rollout.png)

## 7. Passen Sie bei Bedarf Rollout und Traffic-Zuordnung an

Nachdem Sie Ihre Aktivität aktiviert haben, bearbeiten Sie sie jederzeit, um die Traffic-Zuordnung nach Bedarf zu erhöhen oder zu verringern.

Erhöhung der Traffic-Zuordnung von 10 % auf 50 % aufgrund des Erfolgs des ersten Rollouts.

![ALT-Bild](assets/asset-adjust-rollout.png)
