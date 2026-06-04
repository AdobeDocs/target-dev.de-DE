---
keywords: Implementieren, Implementieren, Einrichten, Einrichten, Seitenparameter
description: Abrufen von Daten in  [!DNL Target] mithilfe von In-Page-Profilattributen
title: Wie integriere ich Daten in  [!DNL Target]  mit In-Page-Profilattributen?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
TQID: https://experienceleague.adobe.com/jXWNNl7HfrR03tEoMz7KApX3onc1Zc44IAuXy4QF2tU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 311
ht-degree: 40%

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

[Profilattribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
