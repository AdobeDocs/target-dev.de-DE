---
title: Verwalten benutzerdefinierter Kriterien
description: Schritte, die zur Verwendung von Adobe Target-APIs zum Verwalten, Erstellen, Auflisten, Bearbeiten, Abrufen und Löschen von Adobe Target Recommendations-Kriterien erforderlich sind.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 51a67a49-a92d-4377-9a9f-27116e011ab1
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# Benutzerdefinierte Kriterien verwalten

Manchmal können die von Recommendations bereitgestellten Algorithmen bestimmte Artikel, die beworben werden sollen, nicht aufdecken. In einem solchen Fall bieten benutzerdefinierte Kriterien eine Möglichkeit, einen bestimmten Satz empfohlener Artikel für ein bestimmtes Schlüsselelement oder eine bestimmte Kategorie bereitzustellen.

Um benutzerdefinierte Kriterien zu erstellen, definieren und importieren Sie die gewünschte Zuordnung zwischen dem Schlüsselelement oder der Schlüsselkategorie und den empfohlenen Elementen. Dieser Vorgang wird im Abschnitt [Dokumentation benutzerdefinierter Kriterien](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html). Wie in dieser Dokumentation beschrieben, können Sie benutzerdefinierte Kriterien über die Target-Benutzeroberfläche erstellen, bearbeiten und löschen. Target bietet jedoch auch eine Reihe benutzerspezifischer Kriterien-APIs, die eine detailliertere Verwaltung Ihrer benutzerspezifischen Kriterien ermöglichen.

>[!WARNING]
>
>Führen Sie für benutzerdefinierte Kriterien entweder alle Aktionen (Erstellen, Bearbeiten, Löschen) für ein bestimmtes benutzerdefiniertes Kriterium mithilfe der APIs durch oder führen Sie alle Aktionen (Erstellen, Bearbeiten, Löschen) über die Benutzeroberfläche durch. Die Verwaltung benutzerdefinierter Kriterien durch eine Kombination aus Benutzeroberfläche und API kann zu widersprüchlichen Informationen oder unerwarteten Ergebnissen führen. Beispielsweise spiegelt das Erstellen eines benutzerdefinierten Kriteriums in der Benutzeroberfläche und dessen anschließende Bearbeitung über die API Ihre Aktualisierungen in der Benutzeroberfläche nicht wider, obwohl sie im Backend aktualisiert werden, wie über die API sichtbar.

## Erstellen benutzerdefinierter Kriterien

So erstellen Sie benutzerdefinierte Kriterien mit dem [Benutzerdefinierte Kriterien-API erstellen](https://developer.adobe.com/target/administer/recommendations-api/#operation/createCriteriaCustom)lautet die Syntax:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Benutzerdefinierte Kriterien, die mit der API Benutzerdefinierte Kriterien erstellen erstellt wurden, wie in dieser Übung beschrieben, werden in der Benutzeroberfläche angezeigt, wo sie beibehalten werden. Sie können sie nicht in der Benutzeroberfläche bearbeiten oder löschen. Sie können sie bearbeiten oder löschen **via API** in beide Richtungen jedoch weiterhin in der Target-Benutzeroberfläche angezeigt. Um die Option zum Bearbeiten oder Löschen über die Benutzeroberfläche beizubehalten, erstellen Sie die benutzerdefinierten Kriterien mithilfe der Benutzeroberfläche pro [die Dokumentation](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html)im Gegensatz zur API &quot;Benutzerdefinierte Kriterien erstellen&quot;.

Fahren Sie erst dann mit den folgenden Schritten fort, nachdem Sie die oben stehende Warnung gelesen haben, und erstellen Sie bequem neue benutzerdefinierte Kriterien, die später nicht aus der Benutzeroberfläche gelöscht werden können.

1. Überprüfen `TENANT_ID` und `API_KEY` für **[!UICONTROL Erstellen benutzerdefinierter Kriterien]** referenzieren Sie die zuvor erstellten Postman-Umgebungsvariablen. Verwenden Sie das folgende Bild zum Vergleich.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

1. Fügen Sie Ihre **body** as **raw** JSON, das den Speicherort Ihrer CSV-Datei für benutzerdefinierte Kriterien definiert. Verwenden Sie das Beispiel im Abschnitt [Benutzerdefinierte Kriterien-API erstellen](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom) Dokumentation als Vorlage, `environmentId` und anderen Werten nach Bedarf. Für dieses Beispiel verwenden wir LAST_PURCHASED als Schlüssel.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

1. Senden Sie die Anfrage und beobachten Sie die Antwort, die die Details der soeben erstellten benutzerdefinierten Kriterien enthält.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

1. Um zu überprüfen, ob Ihre benutzerdefinierten Kriterien erstellt wurden, navigieren Sie in Adobe Target zu **[!UICONTROL Recommendations > Kriterien]** und suchen Sie nach Ihren Kriterien nach Namen oder verwenden Sie die **[!UICONTROL Benutzerdefinierte Kriterien-API auflisten]** im nächsten Schritt.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

In diesem Fall haben wir einen Fehler. Untersuchen wir den Fehler, indem wir die benutzerdefinierten Kriterien genauer untersuchen und die **[!UICONTROL Benutzerdefinierte Kriterien-API auflisten]**.

## Benutzerdefinierte Kriterien auflisten

Um eine Liste aller benutzerdefinierten Kriterien zusammen mit Details zu jedem abzurufen, verwenden Sie die [Benutzerdefinierte Kriterien-API auflisten](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom). Die Syntax lautet:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Überprüfen `TENANT_ID` und `API_KEY` und senden Sie die Anfrage. Beachten Sie in der Antwort die benutzerdefinierte Kriterien-ID sowie Details zur zuvor genannten Fehlermeldung.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

In diesem Fall ist der Fehler aufgetreten, weil die Serverinformationen falsch sind. Das bedeutet, dass Target nicht auf die CSV-Datei zugreifen kann, die die benutzerdefinierte Kriteriendefinition enthält. Bearbeiten wir die benutzerdefinierten Kriterien, um dies zu korrigieren.

## Benutzerdefinierte Kriterien bearbeiten

Um die Details einer benutzerdefinierten Kriteriendefinition zu ändern, verwenden Sie die [Benutzerdefinierte Kriterien-API bearbeiten](https://developer.adobe.com/target/administer/recommendations-api/#operation/updateCriteriaCustom). Die Syntax lautet:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Überprüfen `TENANT_ID` und `API_KEY`, wie zuvor.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Geben Sie die Kriterien-ID der (einzelnen) benutzerdefinierten Kriterien an, die Sie bearbeiten möchten.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Geben Sie im Hauptteil aktualisierte JSON-Dateien mit den richtigen Serverinformationen ein. (Geben Sie für diesen Schritt den FTP-Zugriff auf einen Server an, auf den Sie zugreifen können.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Senden Sie die Anfrage und notieren Sie die Antwort.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Überprüfen wir anhand des Erfolgs der aktualisierten benutzerdefinierten Kriterien. **[!UICONTROL Abrufen der API für benutzerdefinierte Kriterien]**.

## Abrufen benutzerdefinierter Kriterien

Um benutzerdefinierte Kriteriendetails für ein bestimmtes benutzerdefiniertes Kriterium anzuzeigen, verwenden Sie die [Abrufen der API für benutzerdefinierte Kriterien](https://developer.adobe.com/target/administer/recommendations-api/#operation/getCriteriaCustom). Die Syntax lautet:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Geben Sie die Kriterien-ID der benutzerdefinierten Kriterien an, deren Details Sie erhalten möchten. Senden Sie die Anfrage und überprüfen Sie die Antwort.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Überprüfen Sie den Erfolg. (Überprüfen Sie in diesem Fall, ob keine weiteren FTP-Fehler mehr vorliegen.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Optional) Überprüfen Sie, ob die Aktualisierung in der Benutzeroberfläche korrekt angezeigt wird.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Benutzerdefinierte Kriterien löschen

Löschen Sie mithilfe der zuvor angegebenen Kriterien-ID Ihre benutzerdefinierten Kriterien mithilfe der [Benutzerdefinierte Kriterien-API löschen](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteCriteriaCustom). Die Syntax lautet:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Geben Sie die Kriterien-ID des (einzelnen) benutzerdefinierten Kriteriums an, das Sie löschen möchten. Klicken Sie auf **[!UICONTROL Senden]**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Vergewissern Sie sich, dass die Kriterien mit &quot;Benutzerdefinierte Kriterien abrufen&quot;gelöscht wurden.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
In diesem Fall zeigt der erwartete 404-Fehler an, dass die gelöschten Kriterien nicht gefunden werden können.

>[!NOTE]
>
>Zur Erinnerung: Die Kriterien werden nicht aus der Target-Benutzeroberfläche entfernt, obwohl sie gelöscht wurden, da sie mit der API Benutzerdefinierte Kriterien erstellen erstellt wurden.

Herzlichen Glückwunsch! Sie können jetzt mithilfe der Recommendations-API Details zu benutzerdefinierten Kriterien erstellen, auflisten, bearbeiten, löschen und abrufen. Im nächsten Abschnitt verwenden Sie die Target-Bereitstellungs-API, um Empfehlungen abzurufen.

&lt;!— [Weiter mit &quot;Abrufen von Recommendations mit der serverseitigen Bereitstellungs-API&quot;>](fetch-recs-server-side-delivery-api.md) —>
