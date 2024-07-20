---
title: Verwalten Ihres Recommendations-Katalogs mithilfe von APIs
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

# Verwalten Ihres Recommendations-Katalogs mithilfe von APIs

Während Sie sicherstellen, dass Sie die [Anforderungen für die Verwendung der Recommendations-API](/help/dev/before-administer/recs-api/overview.md#prerequisites) erfüllen, haben Sie gelernt, wie Sie [ mithilfe des JWT-Authentifizierungsflusses ein Zugriffstoken ](/help/dev/before-administer/configure-authentication.md) generieren, um die [!DNL Adobe Target] Admin-APIs auf der [Adobe Developer Console](https://developer.adobe.com/console/home) zu verwenden.

Sie können jetzt die [Recommendations-APIs](https://developer.adobe.com/target/administer/recommendations-api/) verwenden, um Artikel in Ihrem Empfehlungskatalog hinzuzufügen, zu aktualisieren oder zu löschen. Wie bei den anderen Adobe Target Admin-APIs erfordern auch die Recommendations-APIs eine Authentifizierung.

>[!NOTE]
>
>Senden Sie die **[!UICONTROL IMS: JWT Generate + Auth via User Token]** -Anfrage, wann immer Sie Ihr Zugriffstoken zur Authentifizierung aktualisieren müssen, da es nach 24 Stunden abläuft. Anweisungen finden Sie unter [Konfigurieren der Adobe API-Authentifizierung](../configure-authentication.md) .

![JWT3ff](assets/configure-io-target-jwt3ff.png)

Rufen Sie vor dem Fortfahren die [Recommendations Postman-Sammlung](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman) ab.

## Erstellen und Aktualisieren von Elementen mit der API &quot;Entitäten speichern&quot;

Um Ihre Recommendations-Produktdatenbank mit der API anstatt mit CSV-Produkt-Feed- oder Target-Anfragen zu füllen, die auf Produktseiten ausgelöst werden, verwenden Sie die [API &quot;Entitäten speichern&quot;](https://developer.adobe.com/target/administer/recommendations-api/#operation/saveEntities). Diese Anfrage fügt ein Element in einer einzelnen Target-Umgebung hinzu oder aktualisiert es. Die Syntax lautet:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

So können beispielsweise &quot;Save Entities&quot;verwendet werden, um Artikel zu aktualisieren, wenn bestimmte Schwellenwerte erreicht werden (z. B. Werte für Inventar oder Preis), um diese Elemente zu kennzeichnen und zu verhindern, dass sie empfohlen werden.

1. Navigieren Sie zu **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL CONTROL Environments]** , um die Ziel-Umgebungs-ID abzurufen, zu der Sie ein Element hinzufügen oder aktualisieren möchten.

   ![SaveEntities1](assets/SaveEntities01.png)

1. Überprüfen Sie, ob `TENANT_ID` und `API_KEY` auf die zuvor eingerichteten Postman-Umgebungsvariablen verweisen. Verwenden Sie das folgende Bild zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage so, dass sie mit denen in der Abbildung unten übereinstimmen.

   ![SaveEntities3](assets/SaveEntities03.png)

1. Geben Sie Ihren JSON-Code als **Raw**-Code in den **Textkörper** ein. Vergessen Sie nicht, Ihre Umgebungs-ID mit der Variable `environment` anzugeben. (Im folgenden Beispiel ist die Umgebungs-ID 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   Nachfolgend finden Sie ein Beispiel-JSON, das entity.id kit2001 mit den zugehörigen Entitätswerten für ein Toaster Oven-Produkt in die Umgebung 6781 hinzufügt.

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

   Das JSON-Objekt kann skaliert werden, um mehrere Produkte zu senden. Diese JSON gibt beispielsweise zwei Entitäten an.

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

1. Jetzt bist du dran! Verwenden Sie die **[!UICONTROL Save Entities]** -API, um Ihrem Katalog die folgenden Elemente hinzuzufügen. Verwenden Sie die obige JSON-Beispieldatei als Ausgangspunkt. (Sie müssen die JSON-Datei um weitere Entitäten erweitern.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

Sieht so aus, als gehören die letzten beiden Dinge nicht. Untersuchen wir sie mithilfe der **[!UICONTROL Get Entity]** -API und löschen Sie sie bei Bedarf mithilfe der **[!UICONTROL Delete Entities]** -API.

## Abrufen von Elementdetails mit der Get Entity API

Um die Details eines vorhandenen Elements abzurufen, verwenden Sie die [Entitäts-API abrufen](https://developer.adobe.com/target/administer/recommendations-api/#operation/getEntity) . Die Syntax lautet:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Entitätsdetails können jeweils nur für eine Entität abgerufen werden. Sie können &quot;Entität abrufen&quot;verwenden, um zu bestätigen, dass im Katalog Aktualisierungen wie erwartet vorgenommen wurden, oder um anderweitig den Inhalt des Katalogs zu überprüfen.

1. Geben Sie in der API-Anfrage die Entitäts-ID mithilfe der Variablen &quot;`entityId`&quot;an. Im folgenden Beispiel werden Details für die Entität zurückgegeben, deren entityId=kit2004 lautet.

   ![GetEntity1](assets/GetEntity1.png)

1. Überprüfen Sie, ob `TENANT_ID` und `API_KEY` auf die zuvor eingerichteten Postman-Umgebungsvariablen verweisen. Verwenden Sie das folgende Bild zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage so, dass sie mit denen in der Abbildung unten übereinstimmen.

   ![GetEntity2](assets/GetEntity2.png)

1. Senden Sie die Anfrage.

   ![GetEntity3](assets/GetEntity3.png)
Wenn Sie eine Fehlermeldung erhalten, dass die Entität nicht gefunden wurde (wie im Beispiel oben gezeigt), überprüfen Sie, ob Sie die Anforderung an die richtige Target-Umgebung senden.



   >[!NOTE]
   >
   >Wenn keine Umgebung explizit angegeben ist, versucht &quot;Get Entity&quot;, die Entität nur aus Ihrer [Standardumgebung](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) abzurufen. Wenn Sie von einer anderen Umgebung als der Standardumgebung abrufen möchten, müssen Sie die Umgebungs-ID angeben.

1. Fügen Sie bei Bedarf den Parameter `environmentId` hinzu und senden Sie die Anfrage erneut.

   ![GetEntity4](assets/GetEntity4.png)

1. Senden Sie eine weitere **[!UICONTROL Get Entity]** -Anfrage, diesmal zur Überprüfung der Entität, deren entityId=kit2005 lautet.

   ![GetEntity5](assets/GetEntity5.png)

Angenommen, Sie entscheiden, dass diese Entitäten aus Ihrem Katalog entfernt werden müssen. Verwenden wir die **[!UICONTROL Delete Entities]**-API.

## Löschen von Elementen mit der API &quot;Entitäten löschen&quot;

Um Elemente aus Ihrem Katalog zu entfernen, verwenden Sie die [API zum Löschen von Entitäten](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteEntities). Die Syntax lautet:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
>
>Die API Entitäten löschen löscht Entitäten, die von Ihnen angegebenen IDs referenziert werden. Wenn keine Entitäts-IDs bereitgestellt werden, werden alle Entitäten in der angegebenen Umgebung gelöscht. Wenn keine Umgebungs-ID angegeben wird, werden Entitäten aus allen Umgebungen gelöscht. Seien Sie vorsichtig!

1. Navigieren Sie zu **[!UICONTROL Target]** > **[!UICONTROL Setup]** > **[!UICONTROL Hosts]** > **[!UICONTROL Environments]** , um die Ziel-Umgebungs-ID abzurufen, aus der Sie Elemente löschen möchten.

   ![DeleteEntities1](assets/SaveEntities01.png)

1. Geben Sie in der API-Anfrage die Entitäts-IDs der Entitäten an, die Sie löschen möchten, unter Verwendung der Syntax &quot;`&ids=[comma-delimited-entity-ids]`&quot;(Abfrageparameter). Trennen Sie beim Löschen mehrerer Entitäten die IDs durch Kommas.

   ![DeleteEntities2](assets/DeleteEntities2.png)

1. Geben Sie die Umgebungs-ID mit der Syntax &quot;`&environment=[environmentId]`&quot;an. Andernfalls werden Entitäten in allen Umgebungen gelöscht.

   ![DeleteEntities3](assets/DeleteEntities3.png)

1. Überprüfen Sie, ob `TENANT_ID` und `API_KEY` auf die zuvor eingerichteten Postman-Umgebungsvariablen verweisen. Verwenden Sie das folgende Bild zum Vergleich. Ändern Sie bei Bedarf die Kopfzeilen und den Pfad in Ihrer API-Anfrage so, dass sie mit denen in der Abbildung unten übereinstimmen.

   ![DeleteEntities4](assets/DeleteEntities4.png)

1. Senden Sie die Anfrage.

   ![DeleteEntities5](assets/DeleteEntities5.png)

1. Überprüfen Sie Ihre Ergebnisse mit **[!UICONTROL Get Entity]**, was jetzt darauf hinweisen sollte, dass die gelöschten Entitäten nicht gefunden werden können.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Herzlichen Glückwunsch! Sie können jetzt die Recommendations-APIs verwenden, um Details zu den Entitäten in Ihrem Katalog zu erstellen, zu aktualisieren, zu löschen und abzurufen. Im nächsten Abschnitt erfahren Sie, wie Sie benutzerdefinierte Kriterien verwalten.

&lt;!— [Weiter mit &quot;Verwalten benutzerdefinierter Kriterien&quot;>](manage-custom-criteria.md) —>
