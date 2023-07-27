---
keywords: implementieren, implementieren, einrichten, einrichten, Seitenparameter
description: Daten abrufen [!DNL Target] mithilfe von Seitenparametern.
title: Wie erhalte ich Daten? [!DNL Target] Verwenden von Seitenparametern?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 38%

---

# Seitenparameter

Seitenparameter (auch &quot;Mbox-Parameter&quot;genannt) sind Name/Wert-Paare, die direkt über den Seiten-Code übergeben werden und nicht im Besucherprofil zur zukünftigen Verwendung gespeichert werden.

Seitenparameter sind nützlich, um Seitendaten an zu senden [!DNL Adobe Target] das nicht mit dem Profil des Besuchers für die zukünftige Verwendung von Targeting gespeichert werden muss. Diese Werte werden stattdessen verwendet, um die Seite oder die Aktion zu beschreiben, die der Benutzer auf der jeweiligen Seite ausgeführt hat.

## Format

Seitenparameter werden an übergeben. [!DNL Target] über einen Server-Aufruf als ein Zeichenfolgen-Name/Wert-Paar. Parameternamen und -werte sind anpassbar (obwohl es einige „reservierte Namen“ für spezifische Anwendungen gibt).

Im Folgenden finden Sie einige Beispiele für Seitenparameter

* `page=productPage`

* `categoryId=homeLoans`

## Anwendungsbeispiele

* **Produktseiten**: Senden Sie Informationen über das angezeigte Produkt (so funktioniert Recommendations).
* **Bestelldetails**: Senden der Bestell-ID, orderTotal usw. zur Auftragserfassung
* **Kategorieaffinität:**[!DNL Target] kategorisierte Informationen an senden, um Kenntnisse über die Affinität des Benutzers zu bestimmten Site-Kategorien zu erhalten.
* **Daten von Drittanbietern:** Informationen aus Drittanbieter-Datenquellen, wie Wetter-Targeting-Anbieter, Kontodaten (z. B. DemandBase), demographische Daten (z. B. Experian) und mehr senden.

## Vorteile der Methode

Daten werden an gesendet [!DNL Target] in Echtzeit und kann für denselben Server-Aufruf verwendet werden, für den die Daten eingehen.

## Einschränkungen

* Erfordert ein Seiten-Code-Update (direkt oder über ein Tag-Management-System).
* Wenn die Daten für die Zielgruppenbestimmung bei einem nachfolgenden Seiten-/Server-Aufruf verwendet werden müssen, müssen sie in ein Profilskript übersetzt werden.
* Abfragezeichenfolgen dürfen nur Zeichen des [IETF-Standards](https://www.ietf.org/rfc/rfc3986.txt) (Internet Engineering Task Force) enthalten .

  Zusätzlich zu den Zeichen, die auf der IETF-Site erwähnt werden, [!DNL Target] erlaubt die folgenden Zeichen in Abfragezeichenfolgen:

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

  Alle anderen Zeichen müssen URL-codiert sein. Der Standard gibt das folgende Format an ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ), wie unten dargestellt:

  ![ALT-Bild](assets/ietf1.png)

  Hier auch die vollständige Liste:

  ![ALT-Bild](assets/ietf2.png)

## Codebeispiele

targetPageParamsAll (hängt die Parameter an alle Mbox-Aufrufe auf der Seite an):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (hängt die Parameter an die globale Mbox auf der Seite an):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Links zu relevanten Informationen

Recommendations: [Implementierung nach Seitentyp](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html)

Bestellbestätigung: [Konversions-Tracking](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Kategorieaffinität: [Kategorieaffinität](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html)
