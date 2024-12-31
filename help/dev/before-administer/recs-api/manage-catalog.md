---
title: Verwalten des Recommendations-Katalogs mithilfe von APIs
description: Schritte, die zur Verwendung von Adobe Target-APIs zum Erstellen, Aktualisieren, Speichern, Abrufen und Löschen von Entitäten in Ihrem Recommendations-Katalog erforderlich sind.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: aea82607-cde4-456a-8dfb-2967badce455
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Verwalten des Recommendations-Katalogs mithilfe von APIs

Sie haben gelernt, wie Sie mit dem JWT-Authentifizierungsfluss [ein Zugriffstoken generieren](/help/dev/before-administer/configure-authentication.md) die [!DNL Adobe Target]-Admin-APIs auf der [Adobe Developer Console verwenden, um sicherzustellen, dass Sie die [](/help/dev/before-administer/recs-api/overview.md#prerequisites) Anforderungen zur Verwendung der Recommendations-APIs](https://developer.adobe.com/console/home).

Sie können jetzt die [Recommendations-APIs](https://developer.adobe.com/target/administer/recommendations-api/) verwenden, um Elemente in Ihrem Recommendations-Katalog hinzuzufügen, zu aktualisieren oder zu löschen. Wie alle anderen Adobe Target Recommendations Admin-APIs müssen auch diese authentifiziert werden.

>[!NOTE]
>
>Senden Sie die **[!UICONTROL IMS: JWT Generate + Auth via User Token]**-Anfrage immer dann, wenn Sie Ihr Zugriffstoken zur Authentifizierung aktualisieren müssen, da es nach 24 Stunden abläuft. Anweisungen finden [ unter „Konfigurieren der Adobe](../configure-authentication.md)API-Authentifizierung“.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

Bevor Sie fortfahren, rufen Sie die [Recommendations Postman-Sammlung](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman) ab.

## Erstellen und Aktualisieren von Elementen mit der API zum Speichern von Entitäten

Um Ihre Recommendations-Produktdatenbank mithilfe der API anstelle eines CSV-Produkt-Feeds oder mit Target-Anfragen aufzufüllen, die auf Produktseiten ausgelöst werden, verwenden Sie die [Entitäten-API speichern](https://developer.adobe.com/target/administer/recommendations-api/#operation/saveEntities). Diese Anfrage fügt ein Element in einer einzigen Target-Umgebung hinzu oder aktualisiert es. Die Syntax lautet:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Zum Beispiel können „Entitäten speichern“ verwendet werden, um Artikel zu aktualisieren, wenn bestimmte Schwellenwerte - wie Schwellenwerte für den Bestand oder Preis - erreicht werden, um diese Artikel zu kennzeichnen und zu verhindern, dass sie empfohlen werden.

1. Navigieren Sie zu **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL CONTROL Environments]** , um die Zielumgebungs-ID abzurufen, in der Sie ein Element hinzufügen oder aktualisieren möchten.

   ![SaveEntities1](assets/SaveEntities01.png)

1. Überprüfen Sie, `TENANT_ID` und `API_KEY` auf die zuvor festgelegten Postman-Umgebungsvariablen verweisen. Verwenden Sie die folgende Abbildung zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage, sodass sie denen in der Abbildung unten entsprechen.

   ![SaveEntities3](assets/SaveEntities03.png)

1. Geben Sie Ihre JSON als **Roh**-Code im **Textkörper** ein. Vergessen Sie nicht, Ihre Umgebungs-ID mithilfe der Variablen `environment` anzugeben. (Im folgenden Beispiel ist die Umgebungs-ID 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   Nachfolgend finden Sie ein JSON-Beispiel, das entity.id kit2001 mit zugehörigen Entitätswerten für ein Toaster-Ofen-Produkt in die Umgebung 6781 hinzufügt.

   ```
       {
       "entities": [{
               "name": "Toaster Oven",
               "id": "kit2001",
               "environment": 6781,
               "categories": [
                   "housewares:appliances"
               ],
               "attributes": {
                   "inventory": 77,
                   "margin": 23,
                   "message": "crashing helicopter",
                   "pageUrl": "www.foobar.foo.com/helicopter.html",
                   "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
               }
           }]
       }
   ```

1. Klicken Sie auf **[!UICONTROL Send]**. Sie sollten die folgende Antwort erhalten.

   ![SaveEntities5.png](assets/SaveEntities05.png)

   Das JSON-Objekt kann skaliert werden, um mehrere Produkte zu senden. Diese JSON-Datei gibt beispielsweise zwei Entitäten an.

   ```
       {
           "entities": [{
                   "name": "Toaster Oven",
                   "id": "kit2001",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 89,
                       "margin": 11,
                       "message": "Toaster Oven",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 102.5
                   }
               },
               {
                   "name": "Blender",
                   "id": "kit2002",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 36,
                       "margin": 5,
                       "message": "Blender",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 54.5
                   }
               }
           ]
       }
   ```

1. Jetzt seid ihr dran! Verwenden Sie die **[!UICONTROL Save Entities]**-API, um die folgenden Elemente zu Ihrem Katalog hinzuzufügen. Verwenden Sie die obige Beispiel-JSON als Ausgangspunkt. (Sie müssen die JSON-Datei erweitern, um zusätzliche Entitäten einzuschließen.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

Die letzten beiden Elemente gehören anscheinend nicht dazu. Sehen wir uns diese mithilfe der **[!UICONTROL Get Entity]**-API an und löschen Sie sie ggf. mithilfe der **[!UICONTROL Delete Entities]**-API.

## Abrufen von Elementdetails mit der Get Entity API

Um die Details eines vorhandenen Elements abzurufen, verwenden Sie die [Entitäts-API](https://developer.adobe.com/target/administer/recommendations-api/#operation/getEntity). Die Syntax lautet:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Entitätsdetails können jeweils nur für eine Entität abgerufen werden. Sie können Entität abrufen verwenden, um zu bestätigen, dass Aktualisierungen im Katalog erwartungsgemäß vorgenommen wurden, oder um anderweitig den Inhalt des Katalogs zu überprüfen.

1. Geben Sie in der API-Anfrage die Entitäts-ID mithilfe der Variablen `entityId` an. Das folgende Beispiel gibt Details für die Entität zurück, deren entityId=kit2004 ist.

   ![GetEntity1](assets/GetEntity1.png)

1. Überprüfen Sie, `TENANT_ID` und `API_KEY` auf die zuvor festgelegten Postman-Umgebungsvariablen verweisen. Verwenden Sie die folgende Abbildung zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage, sodass sie denen in der Abbildung unten entsprechen.

   ![GetEntity2](assets/GetEntity2.png)

1. Senden Sie die Anfrage.

   ![GetEntity3](assets/GetEntity3.png)
Wenn Sie einen Fehler erhalten, der besagt, dass die Entität nicht gefunden wurde, wie im Beispiel oben gezeigt, überprüfen Sie, ob Sie die Anfrage an die richtige Zielumgebung senden.



   >[!NOTE]
   >
   >Wenn keine Umgebung explizit angegeben ist, versucht Get Entity, die Entität nur aus Ihrer [Standardumgebung“ ](https://experienceleague.adobe.com/docs/target/using/administer/environments.html). Wenn Sie aus einer anderen Umgebung als der Standardumgebung abrufen möchten, müssen Sie die Umgebungs-ID angeben.

1. Fügen Sie bei Bedarf den `environmentId` Parameter hinzu und senden Sie die Anfrage erneut.

   ![GetEntity4](assets/GetEntity4.png)

1. Senden Sie eine weitere **[!UICONTROL Get Entity]**-Anfrage, dieses Mal, um die Entität zu überprüfen, deren entityId=kit2005 ist.

   ![GetEntity5](assets/GetEntity5.png)

Angenommen, Sie entscheiden, dass diese Entitäten aus Ihrem Katalog entfernt werden müssen. Verwenden wir die **[!UICONTROL Delete Entities]**-API.

## Löschen von Elementen mit der Delete Entities-API

Um Elemente aus Ihrem Katalog zu entfernen, verwenden Sie die [Entitäten löschen-API](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteEntities). Die Syntax lautet:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
>
>Die Delete Entities-API löscht Entitäten, auf die von den von Ihnen angegebenen IDs verwiesen wird. Wenn keine Entitäts-IDs angegeben werden, werden alle Entitäten in der angegebenen Umgebung gelöscht. Wenn keine Umgebungs-ID angegeben wird, werden Entitäten aus allen Umgebungen gelöscht. Verwenden Sie dies mit Vorsicht!

1. Navigieren Sie zu **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL Environments]** , um die Zielumgebungs-ID abzurufen, aus der Sie Elemente löschen möchten.

   ![DeleteEntities1](assets/SaveEntities01.png)

1. Geben Sie in der API-Anfrage die Entitäts-IDs der Entitäten an, die Sie löschen möchten, indem Sie die `&ids=[comma-delimited-entity-ids]` (einen Abfrageparameter) verwenden. Wenn Sie mehr als eine Entität löschen, trennen Sie die IDs durch Kommas.

   ![DeleteEntities2](assets/DeleteEntities2.png)

1. Geben Sie die Umgebungs-ID mithilfe der `&environment=[environmentId]` an. Andernfalls werden Entitäten aus allen Umgebungen gelöscht.

   ![DeleteEntities3](assets/DeleteEntities3.png)

1. Überprüfen Sie, `TENANT_ID` und `API_KEY` auf die zuvor festgelegten Postman-Umgebungsvariablen verweisen. Verwenden Sie die folgende Abbildung zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage, sodass sie denen in der Abbildung unten entsprechen.

   ![DeleteEntities4](assets/DeleteEntities4.png)

1. Senden Sie die Anfrage.

   ![DeleteEntities5](assets/DeleteEntities5.png)

1. Überprüfen Sie Ihre Ergebnisse mit **[!UICONTROL Get Entity]**, das nun anzeigen sollte, dass die gelöschten Entitäten nicht gefunden werden können.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Herzlichen Glückwunsch! Sie können jetzt die Recommendations-APIs verwenden, um Details zu den Entitäten in Ihrem Katalog zu erstellen, zu aktualisieren, zu löschen und zu erhalten. Im nächsten Abschnitt erfahren Sie, wie Sie benutzerdefinierte Kriterien verwalten.

&lt;!— [Nächste „Benutzerdefinierte Kriterien verwalten“ >](manage-custom-criteria.md) —>
