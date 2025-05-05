---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Seitenparameter
description: Abrufen von Daten in  [!DNL Target] mithilfe von In-Page-Profilattributen
title: Wie integriere ich Daten in  [!DNL Target]  mit In-Page-Profilattributen?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%

---

# In-Page-Profilattribute

Bei In-Page-Profilattributen in [!DNL Adobe Target] (auch als „In-Mbox-Profilattribute“ bezeichnet) handelt es sich um Name/Wert-Paare, die direkt durch den Seiten-Code übergeben werden und im Besucherprofil für die zukünftige Verwendung gespeichert werden.

Die Profilattribute auf der Seite erlauben es, benutzerspezifische Daten im Profil von Target zu speichern, um sie später für ein Targeting gezielt zu segmentieren.

## Format

Seiteninterne Profilattribute werden über einen Server-Aufruf als Zeichenfolgenname/Wert-Paar mit dem Präfix „profile“ an [!DNL Target] übergeben. vor dem Attributnamen an Target übergeben.

Attributnamen und -werte sind anpassbar (obwohl es einige „reservierte Namen“ für bestimmte Verwendungszwecke gibt).

Im Folgenden finden Sie einige Beispiele für In-Page-Profilattribute:

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Anwendungsbeispiele

* **Anmeldeinformationen**: Geben Sie Nicht-personenbezogene Daten (personenbezogene Daten) basierend auf der Anmeldung des Benutzers an [!DNL Target] weiter. Bei diesen Daten kann es sich um den Mitgliedschaftsstatus, den Bestellverlauf oder mehr handeln.
* **Store-Info:** verfolgen, welcher Store der bevorzugte Standort dieses Benutzers ist.
* **Bisherige Interaktionen**: verfolgen, was der Benutzer zuvor auf der Site getan hat, um die künftige Personalisierung vorzubereiten.

## Vorteile der -Methode

Daten werden in Echtzeit an [!DNL Target] gesendet und können mit demselben Server-Aufruf verwendet werden, über den auch die Daten eingehen.

## Einschränkungen

Erfordert Seiten-Code-Updates (direkt oder über ein Tag-Management-System).

Attribute und Werte sind in Server-Aufrufen sichtbar, sodass ein Besucher die Werte sehen kann. Beim Austausch von Informationen wie Kreditbereichen oder anderen potenziell privaten Informationen ist diese Methode möglicherweise nicht der beste Ansatz.

## Code-Beispiele

targetPageParamsAll (hängt die Attribute an alle Mbox-Aufrufe auf der Seite an):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (hängt die Attribute an die globale Mbox auf der Seite an):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Attribute im mboxCreate-Code:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Links zu relevanten Informationen

[Profilattribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=de)

[Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=de)
