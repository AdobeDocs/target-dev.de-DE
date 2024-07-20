---
title: Übersicht über die API für Adobe-Modelle
description: Übersicht über die Modelle-API, mit der Benutzer verhindern können, dass Funktionen in Modelle für maschinelles Lernen einbezogen werden.
exl-id: e34b9b03-670b-4f7c-a94e-0c3cb711d8e4
feature: APIs/SDKs, Recommendations, Administration & Configuration
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 2%

---

# Übersicht über die Modelle-API

Mit der Models-API, auch als Blockierungsliste-API bezeichnet, können Benutzer die Liste der Funktionen anzeigen und verwalten, die in Modellen für das maschinelle Lernen für Aktivitäten vom Typ [!UICONTROL Automated Personalization] (AP) und [!DNL Auto-Target] (AT) verwendet werden. Wenn ein Benutzer eine Funktion davon ausschließen möchte, von den Modellen für AP- oder AT-Aktivitäten verwendet zu werden, kann er die Modelle-API verwenden, um diese Funktion der &quot;Blockierungsliste&quot;-Seite hinzuzufügen.

Ein **[!UICONTROL blocklist]** definiert den Satz von Funktionen, die von [!DNL Adobe Target] aus seinen Modellen für maschinelles Lernen ausgeschlossen werden. Weitere Informationen zu Funktionen finden Sie unter [Von [!DNL Target] Algorithmen für maschinelles Lernen verwendete Daten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/ap-data.html).

Blockierungslisten können pro Aktivität (Aktivitätsebene) oder für alle Aktivitäten innerhalb eines [!DNL Target] -Kontos (globale Ebene) definiert werden.

<!-- To get started with the Models API in order to create and manage your blocklist, download the Postman Collection [here](https://git.corp.adobe.com/target/ml-configuration-management-service/tree/nextRelease/rest_api_library). Note this is an Adobe internal link. Need to publish this publicly if want to share with customers. -->

## API-Spezifikation für Modelle

Sehen Sie sich die API-Spezifikation für Modelle [hier](../administer/models-api/models-api-overview.md) an.

## Voraussetzungen 

Um die Modelle-API zu verwenden, müssen Sie die Authentifizierung mit [Adobe Developer Console](https://developer.adobe.com/console/home) konfigurieren, genau wie mit der [Target Admin-API](../administer/admin-api/admin-api-overview-new.md). Weitere Informationen finden Sie unter [Konfigurieren der Authentifizierung](../before-administer/configure-authentication.md).

## Richtlinien zur API-Nutzung von Modellen

Verwalten von Blockierungslisten

[**Schritt 1:**](#step1) Liste der Funktionen für eine Aktivität anzeigen

[**Schritt 2:**](#step2) Überprüfen Sie die Blockierungsliste der Aktivität

[**Schritt 3:**](#step3) Fügen Sie der Blockierungsliste der Aktivität Funktionen hinzu.

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
>Um die Aktivitäts-ID Ihrer Aktivität zu finden, navigieren Sie zur Aktivitätenliste in der Benutzeroberfläche von [!DNL Target] . Klicken Sie auf die gewünschte Aktivität. Die Aktivitäts-ID wird im Hauptteil der resultierenden Aktivitäts-Übersichtsseite sowie am Ende der URL für diese Seite angezeigt.

Der **[!UICONTROL externalName]** ist ein benutzerfreundlicher Name für eine Funktion. Sie wird von [!DNL Target] erstellt und es ist möglich, dass sich dieser Wert im Laufe der Zeit ändert. Benutzer können diese benutzerfreundlichen Namen im [Personalization Insights-Bericht](https://experienceleague.adobe.com/docs/target/using/reports/insights/personalization-insights-reports.html) anzeigen.

Die **[!UICONTROL internalName]** ist die tatsächliche Kennung der Funktion. Er wird auch von [!DNL Target] erstellt, kann jedoch nicht geändert werden. Dies ist der Wert, den Sie referenzieren müssen, um die Funktion(en) zu identifizieren, die Sie Blockierungslisten vornehmen möchten.

Beachten Sie, dass eine Aktivität, damit die Funktionsliste mit Werten aufgefüllt werden kann (d. h. damit sie nicht null ist):

1. Muss Status = Live haben oder zuvor aktiviert worden sein
1. Muss lange genug ausgeführt worden sein, damit eine Kampagnenaktivität vorhanden ist, damit das Modell über Daten verfügt, die ausgeführt werden können.

## Schritt 2: Überprüfen der Blockierungsliste der Aktivität {#step2}

Zeigen Sie als Nächstes die Blockierungsliste an. Überprüfen Sie also, welche Funktionen (sofern vorhanden) derzeit von der Einbeziehung in die Modelle für diese Aktivität ausgeschlossen sind.

>[!ERROR]
>
>Beachten Sie, dass bei `/blockList/` in der Anfrage zwischen Groß- und Kleinschreibung unterschieden wird.

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
>Es können leere Ergebnisse wie diese angezeigt werden, wenn Sie die vollständige Blockierungsliste zum ersten Mal überprüfen, bevor Sie Funktionen hinzufügen. Nachdem Sie jedoch Funktionen aus einer Blockierungsliste hinzugefügt (und anschließend entfernt) haben, werden möglicherweise etwas andere Ergebnisse angezeigt, in denen ein leeres Array mit auf die Blockierungsliste gesetzt Funktionen zurückgegeben wird. Lesen Sie weiter, um ein Beispiel dafür in [Schritt 4](#step4) anzuzeigen.

## Schritt 3: Hinzufügen von Funktionen zur Blockierungsliste &quot;&quot;der Aktivität {#step3}

Um der Blockierungsliste Funktionen hinzuzufügen, ändern Sie die Anforderung von GET in PUT und ändern Sie den Text der Anforderung, um die `blockedFeatureSources` oder `blockedFeatures` anzugeben.

* Der Hauptteil der Anfrage erfordert entweder `blockedFeatures` oder `blockedFeatureSources`. Beide können einbezogen werden.
* Füllen Sie `blockedFeatures` mit Werten, die aus `internalName` identifiziert werden. Siehe [Schritt 1](#step1).
* Füllen Sie `blockedFeatureSources` mit Werten aus der unten stehenden Tabelle.

Beachten Sie, dass `blockedFeatureSources` angibt, woher eine Funktion stammt. Zum Zwecke der auf die Blockierungsliste setz dienen sie als Gruppen oder Funktionskategorien, mit denen Benutzer ganze Funktionssätze gleichzeitig blockieren können. Die Werte von `blockedFeatureSources` stimmen mit den ersten Zeichen der Kennung einer Funktion (`blockedFeatures` - oder `internalName` -Werte) überein. Daher können sie auch als &quot;Feature-Präfixe&quot;betrachtet werden.

### Tabelle der Werte für `blockedFeatureSources` {#table}

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

In dem hier gezeigten Beispiel blockiert der Benutzer zwei Funktionen, `SES_PREVIOUS_VISIT_COUNT` und `SES_TOTAL_SESSIONS`, die er zuvor durch Abfrage der vollständigen Liste der Funktionen für die Aktivität mit der Aktivitäts-ID 260480 identifiziert hatte, wie in [Schritt 1](#step1) beschrieben. Sie blockieren auch alle Funktionen, die von Experience Cloud-Segmenten stammen. Dies wird erreicht, indem Funktionen mit dem Präfix &quot;AAM&quot;blockiert werden, wie in der obigen [Tabelle](#table) beschrieben.

![Schritt 3](assets/models-api-step-3.png)

Beachten Sie, dass es nach der Blockierungsauflistung einer Funktion empfohlen wird, die aktualisierte Blockierungsliste zu überprüfen, indem Sie erneut [Schritt 2} ausführen (GET der Blockierungsliste). ](#step2) Überprüfen Sie, ob die Ergebnisse erwartungsgemäß angezeigt werden (überprüfen Sie, ob die Ergebnisse die Funktionen enthalten, die von der neuesten PUT-Anfrage hinzugefügt wurden).

## Schritt 4: (Optional) Block aufheben {#step4}

Um alle auf die Blockierungsliste gesetzt Funktionen zu entsperren, löschen Sie die Werte von `blockedFeatureSources` oder `blockedFeatures`.

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

In dem hier gezeigten Beispiel leert der Benutzer seine Blockierungsliste für die Aktivität, deren Aktivitäts-ID 260840 lautet. Beachten Sie, dass die Antwort leere Arrays sowohl für blockierte Funktionen als auch für ihre Quellen (0 und 1) bestätigt.`blockedFeatureSources``blockedFeatures`

![Schritt 4](assets/models-api-step-4.png)

Wie immer sollten Sie nach dem Ändern der Blockierungsliste [Schritt 2](#step2) erneut durchführen (GET umfasst Funktionen wie erwartet). In dem hier gezeigten Beispiel prüft der Benutzer, ob seine Blockierungsliste jetzt leer ist.

![Schritt 4b](assets/models-api-step-4b.png)

Frage: Wie kann ich einige, aber nicht alle Blockierungslisten löschen?

Antwort: Um eine separate Untergruppe auf die Blockierungsliste gesetzt Funktionen aus einer Multi-Feature-Blockierungsliste zu entfernen, können Benutzer einfach die aktualisierte Liste der Funktionen senden, die sie in [der Blockanfrage](#step3) hinzufügen möchten, anstatt die gesamte Blockierungsliste zu löschen und die gewünschten Funktionen erneut hinzuzufügen. Senden Sie also die aktualisierte Funktionsliste (wie in Schritt 3.1 gezeigt) und schließen Sie dabei die Funktionen aus, die Sie aus der Blockierungsliste &quot;löschen&quot;möchten.[](#step3)

## Schritt 5: (Optional) Globale Blockierungsliste verwalten {#step5}

Die obigen Beispiele befanden sich alle im Kontext einer einzelnen Aktivität. Sie können Funktionen auch für alle Aktivitäten eines bestimmten Clients (Mandanten) blockieren, anstatt die Blockierungsliste für jede Aktivität einzeln angeben zu müssen. Um eine globale Blockierungsliste durchzuführen, verwenden Sie den Aufruf `/blockList/global` anstelle von `blockList/<campaignId>`.

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

In der oben gezeigten Beispielanfrage blockiert der Benutzer zwei Funktionen, &quot;AAM_FEATURE_1&quot;und &quot;AAM_FEATURE_2&quot;, für alle Aktivitäten in seinem [!DNL Target]-Konto. Das bedeutet, dass &quot;AAM_FEATURE_1&quot;und &quot;AAM_FEATURE_2&quot;unabhängig von der Aktivität nicht in die Modelle für maschinelles Lernen für dieses Konto aufgenommen werden. Darüber hinaus blockiert der Benutzer global alle Funktionen, deren Präfix &quot;AAM&quot;, &quot;PRO&quot;oder &quot;ENV&quot;lautet.

Frage: Ist das obige Codebeispiel nicht redundant?

Antwort: Ja. Es ist überflüssig, Funktionen mit Werten zu blockieren, die mit &quot;AAM&quot;beginnen, und gleichzeitig alle Funktionen zu blockieren, deren Quelle &quot;AAM&quot;lautet. Das Ergebnis ist, dass alle von AAM (Experience Cloud-Segmenten) bezogenen Funktionen blockiert werden. Wenn das Ziel darin besteht, alle Funktionen von Experience Cloud-Segmenten zu blockieren, ist es daher nicht erforderlich, bestimmte Funktionen, die mit &quot;AAM&quot;beginnen, einzeln anzugeben, wie im obigen Beispiel gezeigt.

Endlicher Schritt: Es wird empfohlen, die Blockierungsliste nach der Änderung auf Aktivitäts- oder globaler Ebene zu überprüfen, um sicherzustellen, dass sie die erwarteten Werte enthält. Ändern Sie dazu die `PUT` in eine `GET`.

Die unten dargestellte Beispielantwort weist darauf hin, dass [!DNL Target] zwei einzelne Funktionen sowie alle von &quot;AAM&quot;, &quot;PRO&quot;und &quot;ENV&quot;bezogenen Funktionen blockiert.

![Schritt 5](assets/models-api-step-5.png)
