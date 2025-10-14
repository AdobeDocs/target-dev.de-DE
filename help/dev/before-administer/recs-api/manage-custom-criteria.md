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
source-wordcount: '869'
ht-degree: 0%

---

# Verwalten benutzerdefinierter Kriterien

Manchmal können die von Recommendations bereitgestellten Algorithmen bestimmte Elemente, die Sie bewerben möchten, nicht aufdecken. In einem solchen Fall bieten benutzerdefinierte Kriterien eine Möglichkeit, einen bestimmten Satz empfohlener Elemente für ein bestimmtes Schlüsselelement oder eine bestimmte Kategorie bereitzustellen.

Um benutzerdefinierte Kriterien zu erstellen, definieren und importieren Sie die gewünschte Zuordnung zwischen dem Schlüsselelement oder der Kategorie und den empfohlenen Elementen. Dieser Prozess wird in der [Dokumentation zu benutzerdefinierten Kriterien“ &#x200B;](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=de). Wie in dieser Dokumentation erwähnt, können Sie benutzerdefinierte Kriterien über die Benutzeroberfläche von Target erstellen, bearbeiten und löschen. Target bietet jedoch auch eine Reihe von APIs für benutzerdefinierte Kriterien, die eine detailliertere Verwaltung Ihrer benutzerdefinierten Kriterien ermöglichen.

>[!WARNING]
>
>Bei benutzerdefinierten Kriterien führen Sie entweder alle Aktionen (Erstellen, Bearbeiten, Löschen) für ein bestimmtes benutzerdefiniertes Kriterium mithilfe der APIs durch oder führen Sie alle Aktionen (Erstellen, Bearbeiten, Löschen) mithilfe der Benutzeroberfläche durch. Die Verwaltung Ihrer benutzerdefinierten Kriterien über eine Kombination aus Benutzeroberfläche und API kann zu widersprüchlichen Informationen oder unerwarteten Ergebnissen führen. Wenn Sie beispielsweise ein benutzerdefiniertes Kriterium in der Benutzeroberfläche erstellen, es dann aber über die API bearbeiten, werden Ihre Aktualisierungen in der Benutzeroberfläche nicht angezeigt, auch wenn sie im Backend aktualisiert werden, wie über die API sichtbar.

## Erstellen benutzerdefinierter Kriterien

Zum Erstellen benutzerdefinierter Kriterien mit der [API für benutzerdefinierte Kriterien erstellen](https://developer.adobe.com/target/administer/recommendations-api/#operation/createCriteriaCustom) lautet die Syntax:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Benutzerdefinierte Kriterien, die mit der API Benutzerdefinierte Kriterien erstellen erstellt wurden, wie in dieser Übung beschrieben, werden in der Benutzeroberfläche angezeigt, wo sie beibehalten werden. Sie können sie nicht in der Benutzeroberfläche bearbeiten oder löschen. Sie können sie bearbeiten oder löschen **über die API**, aber in beiden Fällen werden sie weiterhin in der Target-Benutzeroberfläche angezeigt. Damit die Option zum Bearbeiten oder Löschen aus der Benutzeroberfläche beibehalten werden kann, erstellen Sie die benutzerdefinierten Kriterien mithilfe der Benutzeroberfläche gemäß [Dokumentation](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=de) im Gegensatz zur Verwendung der API zum Erstellen benutzerdefinierter Kriterien.

Fahren Sie mit den folgenden Schritten erst fort, nachdem Sie die obige Warnung gelesen haben und neue benutzerdefinierte Kriterien erstellen, die anschließend nicht aus der Benutzeroberfläche gelöscht werden können.

1. Überprüfen Sie `TENANT_ID` und `API_KEY` für **[!UICONTROL Create custom criteria]** Verweis auf die zuvor festgelegten Postman-Umgebungsvariablen. Verwenden Sie die folgende Abbildung zum Vergleich.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

1. Fügen Sie Ihren **Textkörper** als **Roh**-JSON hinzu, das den Speicherort Ihrer benutzerdefinierten CSV-Kriteriendatei definiert. Verwenden Sie das Beispiel in der Dokumentation [Erstellen benutzerdefinierter Kriterien](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom) als Vorlage und geben Sie Ihre `environmentId` und andere Werte nach Bedarf an. In diesem Beispiel verwenden wir LAST_PURCHASED als Schlüssel.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

1. Senden Sie die Anfrage und beobachten Sie die Antwort, die die Details der soeben erstellten benutzerdefinierten Kriterien enthält.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

1. Um zu überprüfen, ob Ihre benutzerdefinierten Kriterien erstellt wurden, navigieren Sie in Adobe Target zu **[!UICONTROL Recommendations > Criteria]** und suchen Sie anhand des Namens nach Ihren Kriterien, oder verwenden Sie die **[!UICONTROL List Custom Criteria API]** im nächsten Schritt.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

In diesem Fall liegt ein Fehler vor. Untersuchen wir den Fehler, indem wir die benutzerdefinierten Kriterien mithilfe der **[!UICONTROL List Custom Criteria API]** genauer untersuchen.

## Benutzerdefinierte Kriterien auflisten

Um eine Liste aller benutzerdefinierten Kriterien zusammen mit Details für jedes abzurufen, verwenden Sie die [API für benutzerdefinierte Kriterien auflisten](https://developer.adobe.com/target/administer/recommendations-api/#operation/getAllCriteriaCustom). Die Syntax lautet:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Überprüfen Sie `TENANT_ID` und `API_KEY` wie zuvor und senden Sie die Anfrage. Beachten Sie in der Antwort die Kennung der benutzerdefinierten Kriterien sowie Details zur zuvor erwähnten Fehlermeldung.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

In diesem Fall ist der Fehler aufgetreten, weil die Server-Informationen falsch sind, d. h. Target kann nicht auf die CSV-Datei zugreifen, die die benutzerdefinierte Kriteriendefinition enthält. Bearbeiten wir die benutzerdefinierten Kriterien, um dies zu korrigieren.

## Benutzerdefinierte Kriterien bearbeiten

Um die Details einer benutzerdefinierten Kriteriendefinition zu ändern, verwenden Sie die [API für benutzerdefinierte Kriterien bearbeiten](https://developer.adobe.com/target/administer/recommendations-api/#operation/updateCriteriaCustom). Die Syntax lautet:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Überprüfen Sie `TENANT_ID` und `API_KEY` wie zuvor.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Geben Sie die Kriterien-ID der (einzelnen) benutzerdefinierten Kriterien an, die Sie bearbeiten möchten.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Geben Sie im Textkörper aktualisierte JSON-Dateien mit den richtigen Server-Informationen ein. (Geben Sie für diesen Schritt den FTP-Zugriff auf einen Server an, auf den Sie zugreifen können.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Senden Sie die Anfrage und notieren Sie die Antwort.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Überprüfen wir den Erfolg der aktualisierten benutzerdefinierten Kriterien mithilfe der **[!UICONTROL Get Custom Criteria API]**.

## Abrufen benutzerdefinierter Kriterien

Um Details zu benutzerdefinierten Kriterien für bestimmte benutzerdefinierte Kriterien anzuzeigen, verwenden Sie die [API für benutzerdefinierte Kriterien abrufen](https://developer.adobe.com/target/administer/recommendations-api/#operation/getCriteriaCustom). Die Syntax lautet:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Geben Sie die Kriterien-ID der benutzerdefinierten Kriterien an, deren Details Sie erhalten möchten. Senden Sie die Anfrage und überprüfen Sie die Antwort.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Überprüfen Sie den Erfolg. (Stellen Sie in unserem Fall sicher, dass keine weiteren FTP-Fehler vorliegen.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Optional) Überprüfen Sie, ob die Aktualisierung korrekt in der Benutzeroberfläche angezeigt wird.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Benutzerdefinierte Kriterien löschen

Löschen Sie mithilfe der zuvor erwähnten Kriterien-ID Ihre benutzerdefinierten Kriterien mithilfe der [API für benutzerdefinierte Kriterien löschen](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteCriteriaCustom). Die Syntax lautet:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Geben Sie die Kriterien-ID der (einzelnen) benutzerdefinierten Kriterien an, die Sie löschen möchten. Klicken Sie auf **[!UICONTROL Send]**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Stellen Sie sicher, dass die Kriterien mit Benutzerdefinierte Kriterien abrufen gelöscht wurden.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
In diesem Fall zeigt der erwartete 404-Fehler an, dass die gelöschten Kriterien nicht gefunden wurden.

>[!NOTE]
>
>Zur Erinnerung: Die Kriterien werden nicht aus der Target-Benutzeroberfläche entfernt, obwohl sie gelöscht wurden, da sie mit der API für benutzerdefinierte Kriterien erstellen erstellt wurden.

Herzlichen Glückwunsch! Sie können jetzt mithilfe der Recommendations-API benutzerdefinierte Kriterien erstellen, auflisten, bearbeiten, löschen und Details dazu abrufen. Im nächsten Abschnitt verwenden Sie die Target-Bereitstellungs-API zum Abrufen von Empfehlungen.

&lt;!— [Weiter &quot;Recommendations mit der Server-seitigen Bereitstellungs-API abrufen“ >](fetch-recs-server-side-delivery-api.md) —>
