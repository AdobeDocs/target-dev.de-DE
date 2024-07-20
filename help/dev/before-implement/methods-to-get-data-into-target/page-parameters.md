---
keywords: implementieren, implementieren, einrichten, einrichten, Seitenparameter
description: Rufen Sie Daten mithilfe von Seitenparametern in [!DNL Target] ab.
title: Wie kann ich Daten mithilfe von Seitenparametern in [!DNL Target] einbringen?
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 32%

---

# Seitenparameter

Seitenparameter (auch &quot;Mbox-Parameter&quot;genannt) sind Name/Wert-Paare, die direkt über den Seiten-Code übergeben werden und nicht im Besucherprofil zur zukünftigen Verwendung gespeichert werden.

Seitenparameter sind nützlich, um Seitendaten an [!DNL Adobe Target] zu senden, die nicht mit dem Profil des Besuchers gespeichert werden müssen, um sie für die zukünftige Zielgruppenbestimmung verwenden zu können. Diese Werte werden stattdessen verwendet, um die Seite oder die Aktion zu beschreiben, die der Benutzer auf der jeweiligen Seite ausgeführt hat.

## Format

Seitenparameter werden über einen Server-Aufruf als Name/Wert-Paar der Zeichenfolge an [!DNL Target] übergeben. Parameternamen und -werte sind anpassbar (obwohl es einige „reservierte Namen“ für spezifische Anwendungen gibt).

Im Folgenden finden Sie einige Beispiele für Seitenparameter

* `page=productPage`

* `categoryId=homeLoans`

## Anwendungsbeispiele

* **Produktseiten**: Senden Sie Informationen über das angezeigte Produkt (so funktioniert Recommendations).
* **Bestelldetails**: Bestell-ID, orderTotal usw. für die Auftragserfassung senden
* **Kategorieaffinität**: Senden Sie kategorisierte Informationen an [!DNL Target], um Kenntnisse über die Affinität des Benutzers zu bestimmten Site-Kategorien zu erhalten.
* **Daten von Drittanbietern:** Informationen aus Drittanbieter-Datenquellen, wie Wetter-Targeting-Anbieter, Kontodaten (z. B. DemandBase), demographische Daten (z. B. Experian) und mehr senden.

## Vorteile der Methode

Daten werden in Echtzeit an [!DNL Target] gesendet und können für denselben Server-Aufruf verwendet werden, für den die Daten eingehen.

## Einschränkungen

* Erfordert ein Seiten-Code-Update (direkt oder über ein Tag-Management-System).
* Wenn die Daten für die Zielgruppenbestimmung bei einem nachfolgenden Seiten-/Server-Aufruf verwendet werden müssen, müssen sie in ein Profilskript übersetzt werden.
* Abfragezeichenfolgen dürfen nur Zeichen gemäß dem [IETF (Internet Engineering Task Force)-Standard](https://www.ietf.org/rfc/rfc3986.txt) enthalten.

  Zusätzlich zu den auf der IETF-Site erwähnten Zeichen erlaubt [!DNL Target] die folgenden Zeichen in Abfragezeichenfolgen:

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

  Alle anderen Zeichen müssen URL-codiert sein. Der Standard gibt das folgende Format ( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) ) an, wie unten dargestellt:

  ![alt image](assets/ietf1.png)

  Hier auch die vollständige Liste:

  ![alt image](assets/ietf2.png)

## Codebeispiele

targetPageParamsAll (hängt die Parameter an alle Mbox-Aufrufe auf der Seite an):

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams (hängt die Parameter an die globale Mbox auf der Seite an):

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## Links zu relevanten Informationen

Recommendations: [Implementierung nach Seitentyp](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html)

Bestellbestätigung: [Konversions-Tracking](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

Kategorieaffinität: [Kategorieaffinität](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html)
