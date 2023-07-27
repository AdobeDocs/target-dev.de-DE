---
title: Übersicht über die API für Adobe-Modelle
description: Übersicht über die Modelle-API, mit der Benutzer verhindern können, dass Funktionen in Modelle für maschinelles Lernen einbezogen werden.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 2%

---

# Übersicht über die Modelle-API

Mit der Models-API, auch als Blockierungsliste-API bezeichnet, können Benutzer die Liste der Funktionen anzeigen und verwalten, die in Modellen für maschinelles Lernen für [!UICONTROL Automated Personalization] AP und [!DNL Auto-Target] (AT) Tätigkeiten. Wenn ein Benutzer eine Funktion davon ausschließen möchte, von den Modellen für AP- oder AT-Aktivitäten verwendet zu werden, kann er die Modelle-API verwenden, um diese Funktion der &quot;Blockierungsliste&quot;-Seite hinzuzufügen.

A **[!UICONTROL Blockierungsliste]** definiert den Satz von Funktionen, die von [!DNL Adobe Target] aus seinen Modellen für maschinelles Lernen. Weitere Informationen zu Funktionen finden Sie unter [Von [!DNL Target] Algorithmen für maschinelles Lernen](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html).

Blockierungslisten können pro Aktivität (Aktivitätsebene) oder für alle Aktivitäten innerhalb einer [!DNL Target] -Konto (globale Ebene).

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## API-Spezifikation für Modelle

API-Spezifikation für Modelle anzeigen [here](../administer/models-api/models-api-overview.md).

## Voraussetzungen 

Um die Modelle-API zu verwenden, müssen Sie die Authentifizierung mithilfe der [Adobe Developer-Konsole](https://developer.adobe.com/console/home), genau wie bei der [Target Admin-API](../administer/admin-api/admin-api-overview-new.md). Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung](../before-administer/configure-authentication.md).

## Richtlinien zur API-Nutzung von Modellen

Verwalten von Blockierungslisten

[**Schritt 1:**](#step1) Liste der Funktionen einer Aktivität anzeigen

[**Schritt 2:**](#step2) Überprüfen der Blockierungsliste der Aktivität

[**Schritt 3:**](#step3) Hinzufügen von Funktionen zur Blockierungsliste der Aktivität

[**Schritt 4:**](#step4) (Optional) Block aufheben

[**Schritt 5:**](#step5) (Optional) Globale Blockierungsliste verwalten


## Schritt 1: Liste der Funktionen einer Aktivität anzeigen {#step1}

Bevor Sie eine Funktion auf die Blockierungsliste gesetzt haben, sollten Sie sich die Liste der Funktionen ansehen, die derzeit in den Modellen für diese Aktivität enthalten sind.

>[!BEGINTABS]

>[!TAB Anfrage]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/<campaignId>
```

>[!TAB Antwort]

```json {line-numbers="true"}
{
    "features": [
        {
            "externalName": "Visitor Profile - Total Visits to Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Total Visits",
            "internalName": "SES_TOTAL_SESSIONS",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Pages Seen Before Activity",
            "internalName": "SES_PREVIOUS_VISIT_COUNT",
            "type": "CONTINUOUS"
        },
        {
            "externalName": "Visitor Profile - Activity Lifetime Time on Site",
            "internalName": "SES_TOTAL_TIME",
            "type": "CONTINUOUS"
        }
    ],
    "reportParameters": {
        "clientCode": <tenant>,
        "campaignId": <campaignId>
    }
}
```

>[!ENDTABS]

<!-- JUDY: Update codeblock above once you have the complete Response. -->

In dem hier gezeigten Beispiel prüft der Benutzer, ob die Liste der Funktionen angezeigt wird, die im Modell für die Aktivität verwendet werden, deren Aktivitäts-ID 260840 lautet.

![Schritt 1](assets/models-api-step-1.png)

>[!NOTE]
>
>Um die Aktivitäts-ID Ihrer Aktivität zu ermitteln, navigieren Sie zur Aktivitätenliste im [!DNL Target] Benutzeroberfläche. Klicken Sie auf die gewünschte Aktivität. Die Aktivitäts-ID wird im Hauptteil der resultierenden Aktivitäts-Übersichtsseite sowie am Ende der URL für diese Seite angezeigt.

Die **[!UICONTROL externalName]** ist ein benutzerfreundlicher Name für eine Funktion. Sie wird von [!DNL Target]und es ist möglich, dass sich dieser Wert im Laufe der Zeit ändert. Die Benutzer können diese benutzerfreundlichen Namen im [Personalization Insights-Bericht](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html).

Die **[!UICONTROL internalName]** ist die tatsächliche Kennung der Funktion. Sie wird auch von [!DNL Target], kann jedoch nicht geändert werden. Dies ist der Wert, den Sie referenzieren müssen, um die Funktion(en) zu identifizieren, die Sie Blockierungslisten vornehmen möchten.

Beachten Sie, dass eine Aktivität, damit die Funktionsliste mit Werten aufgefüllt werden kann (d. h. damit sie nicht null ist):

1. Muss Status = Live haben oder zuvor aktiviert worden sein
1. Muss lange genug ausgeführt worden sein, damit eine Kampagnenaktivität vorhanden ist, damit das Modell über Daten verfügt, die ausgeführt werden können.

## Schritt 2: Überprüfen der Blockierungsliste der Aktivität {#step2}

Zeigen Sie als Nächstes die Blockierungsliste an. Überprüfen Sie also, welche Funktionen (sofern vorhanden) derzeit von der Einbeziehung in die Modelle für diese Aktivität ausgeschlossen sind.

>[!ERROR]
>
>Beachten Sie Folgendes: `/blockList/` in der Anfrage zwischen Groß- und Kleinschreibung unterscheidet.

>[!BEGINTABS]

>[!TAB Anfrage]

```json {line-numbers="true"}
GET https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>
```

>[!TAB Antwort]

```json {line-numbers="true"}

```

>[!ENDTABS]

In dem hier gezeigten Beispiel prüft der Benutzer die Liste der gesperrten Funktionen für die Aktivität, deren Aktivitäts-ID 260840 lautet. Die Ergebnisse sind leer, was bedeutet, dass diese Aktivität derzeit keine auf die Blockierungsliste gesetzt Funktionen aufweist.

![Schritt 2](assets/models-api-step-2.png)

>[!NOTE]
>
>Es können leere Ergebnisse wie diese angezeigt werden, wenn Sie die vollständige Blockierungsliste zum ersten Mal überprüfen, bevor Sie Funktionen hinzufügen. Nachdem Sie jedoch Funktionen aus einer Blockierungsliste hinzugefügt (und anschließend entfernt) haben, werden möglicherweise etwas andere Ergebnisse angezeigt, in denen ein leeres Array mit auf die Blockierungsliste gesetzt Funktionen zurückgegeben wird. Lesen Sie weiter, um ein Beispiel dafür in anzuzeigen. [Schritt 4](#step4).

## Schritt 3: Hinzufügen von Funktionen zur Blockierungsliste &quot;&quot;der Aktivität {#step3}

Um der Blockierungsliste Funktionen hinzuzufügen, ändern Sie die Anforderung von GET in PUT und ändern Sie den Text der Anforderung, um die `blockedFeatureSources` oder `blockedFeatures` nach Bedarf.

* Der Hauptteil der Anfrage erfordert entweder `blockedFeatures` oder `blockedFeatureSources`. Beide können einbezogen werden.
* Auffüllen `blockedFeatures` mit Werten, die aus `internalName`. Siehe [Schritt 1](#step1).
* Auffüllen `blockedFeatureSources` mit Werten aus der unten stehenden Tabelle.

Beachten Sie Folgendes: `blockedFeatureSources` gibt an, woher eine Funktion stammt. Zum Zwecke der auf die Blockierungsliste setz dienen sie als Gruppen oder Funktionskategorien, mit denen Benutzer ganze Funktionssätze gleichzeitig blockieren können. Die Werte von `blockedFeatureSources` Übereinstimmung mit den ersten Zeichen der Kennung einer Funktion (`blockedFeatures` oder `internalName` -Werte); daher können sie auch als &quot;Feature-Präfixe&quot;betrachtet werden.

### Tabelle `blockedFeatureSources` values {#table}

| Präfix | Beschreibung |
| --- | --- |
| BOX | Parameter „mbox“ |
| URL | Benutzerspezifisch - URL-Parameter |
| ENV | Umgebung |
| SES | Besucherprofil |
| GEO | Geo-Position |
| PRO | Benutzerspezifisch - Profil |
| SEG | Benutzerspezifisch - Berichterstellungssegment |
| AAM | Benutzerspezifisch - Experience Cloud-Segment |
| MOB | Mobile |
| CRS | Benutzerspezifisch - Kundenattribute |
| UPA | Benutzerspezifisch - RT-CDP-Profilattribut |
| IAC | Interessensgebiete der Besucher |  |

>[!BEGINTABS]

>[!TAB Anfrage]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": ["AAM"],
    "blockedFeatures": ["SES_PREVIOUS_VISIT_COUNT", "SES_TOTAL_SESSIONS"]
}
```

>[!TAB Antwort]

```json {line-numbers="true"}
{
    "blockedFeatures": [
            "SES_PREVIOUS_VISIT_COUNT",
            "SES_TOTAL_SESSIONS"
        ],
    "blockedFeatureSources": [
            "AAM"
        ]
}
```

>[!ENDTABS]

In dem hier gezeigten Beispiel blockiert der Benutzer zwei Funktionen: `SES_PREVIOUS_VISIT_COUNT` und `SES_TOTAL_SESSIONS`, die sie zuvor durch Abfrage der vollständigen Liste der Funktionen für die Aktivität identifiziert haben, deren Aktivitäts-ID 260480 lautet, wie unter [Schritt 1](#step1). Sie blockieren auch alle Funktionen, die von Experience Cloud-Segmenten kommen. Dies wird erreicht, indem Funktionen mit dem Präfix &quot;AAM&quot;blockiert werden, wie im Abschnitt [table](#table) höher.

![Schritt 3](assets/models-api-step-3.png)

Beachten Sie, dass es nach dem auf die Blockierungsliste setz einer Funktion empfohlen wird, die aktualisierte Blockierungsliste durch [Schritt 2](#step2) erneut (GET der Blockierungsliste). Überprüfen Sie, ob die Ergebnisse erwartungsgemäß angezeigt werden (überprüfen Sie, ob die Ergebnisse die Funktionen enthalten, die von der neuesten PUT-Anfrage hinzugefügt wurden).

## Schritt 4: (Optional) Block aufheben {#step4}

Um alle auf die Blockierungsliste gesetzt Funktionen zu entsperren, löschen Sie die Werte aus `blockedFeatureSources` oder `blockedFeatures`.

>[!BEGINTABS]

>[!TAB Anfrage]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/<campaignId>

{
    "blockedFeatureSources": [],
    "blockedFeatures": []
}
```

>[!TAB Antwort]

```json {line-numbers="true"}
{
    "blockedFeatures": [],
    "blockedFeatureSources": []
}
```

>[!ENDTABS]

In dem hier gezeigten Beispiel leert der Benutzer seine Blockierungsliste für die Aktivität, deren Aktivitäts-ID 260840 lautet. Beachten Sie, dass die Antwort leere Arrays sowohl für blockierte Funktionen als auch für deren Quellen bestätigt —`blockedFeatureSources` und `blockedFeatures`, bzw.

![Schritt 4](assets/models-api-step-4.png)

Wie immer wird nach dem Ändern der Blockierungsliste empfohlen, [Schritt 2](#step2) erneut (GET der Blockierungsliste, um zu überprüfen, ob die Liste Funktionen wie erwartet enthält). In dem hier gezeigten Beispiel prüft der Benutzer, ob seine Blockierungsliste jetzt leer ist.

![Schritt 4b](assets/models-api-step-4b.png)

Frage: Wie kann ich einige, aber nicht alle Blockierungslisten löschen?

Antwort: Um eine separate Untergruppe auf die Blockierungsliste gesetzt Funktionen aus einer Multi-Feature-Blockierungsliste zu entfernen, können Benutzer einfach die aktualisierte Liste der Funktionen senden, die sie blockieren möchten [die Anforderung der Blockierungsliste](#step3)anstatt die gesamte Blockierungsliste zu löschen und die gewünschten Funktionen erneut hinzuzufügen. Senden Sie also die aktualisierte Funktionsliste (wie in [Schritt 3](#step3)), wobei Sie sicherstellen, dass Sie die Funktionen, die Sie &quot;löschen&quot;möchten, aus der Blockierungsliste ausschließen.

## Schritt 5: (Optional) Globale Blockierungsliste verwalten {#step5}

Die obigen Beispiele befanden sich alle im Kontext einer einzelnen Aktivität. Sie können Funktionen auch für alle Aktivitäten eines bestimmten Clients (Mandanten) blockieren, anstatt die Blockierungsliste für jede Aktivität einzeln angeben zu müssen. Um eine globale Blockierungsliste durchzuführen, verwenden Sie die `/blockList/global` Aufruf anstelle von `blockList/<campaignId>`.

>[!BEGINTABS]

>[!TAB Anfrage]

```json {line-numbers="true"}
PUT https://mc.adobe.io/<tenant>/target/models/features/blockList/global

{
    "blockedFeatureSources": ["AAM", "PRO", "ENV"],
    "blockedFeatures": ["AAM_FEATURE_1", "AAM_FEATURE_2"]
}
```

>[!TAB Antwort]

```json {line-numbers="true"}
{
    "blockedFeatures": [
        "AAM_FEATURE_1",
        "AAM_FEATURE_2"
    ],
    "blockedFeatureSources": [
        "AAM",
        "PRO",
        "ENV"
    ]
}
```

>[!ENDTABS]

In der oben gezeigten Beispielanfrage blockiert der Benutzer zwei Funktionen, &quot;AAM_FEATURE_1&quot;und &quot;AAM_FEATURE_2&quot;, für alle Aktivitäten in ihren [!DNL Target] -Konto. Das bedeutet, dass &quot;AAM_FEATURE_1&quot;und &quot;AAM_FEATURE_2&quot;unabhängig von der Aktivität nicht in die Modelle für maschinelles Lernen für dieses Konto aufgenommen werden. Darüber hinaus blockiert der Benutzer global alle Funktionen, deren Präfix &quot;AAM&quot;, &quot;PRO&quot;oder &quot;ENV&quot;lautet.

Frage: Ist das obige Codebeispiel nicht redundant?

Antwort: Ja. Es ist überflüssig, Funktionen mit Werten zu blockieren, die mit &quot;AAM&quot;beginnen, und gleichzeitig alle Funktionen zu blockieren, deren Quelle &quot;AAM&quot;lautet. Das Ergebnis ist, dass alle von AAM (Experience Cloud Segments) bezogenen Funktionen blockiert werden. Wenn das Ziel darin besteht, alle Funktionen von Experience Cloud-Segmenten zu blockieren, ist es daher nicht erforderlich, bestimmte Funktionen, die mit &quot;AAM&quot;beginnen, einzeln anzugeben, wie im obigen Beispiel gezeigt.

Endlicher Schritt: Es wird empfohlen, die Blockierungsliste nach der Änderung auf Aktivitäts- oder globaler Ebene zu überprüfen, um sicherzustellen, dass sie die erwarteten Werte enthält. Ändern Sie dazu die `PUT` zu `GET`.

Die folgende Beispielantwort zeigt [!DNL Target] blockiert zwei einzelne Funktionen sowie alle Funktionen aus &quot;AAM&quot;, &quot;PRO&quot;und &quot;ENV&quot;.

![Schritt 5](assets/models-api-step-5.png)
