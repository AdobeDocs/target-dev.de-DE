---
keywords: implementieren, implementieren, einrichten, einrichten, Seitenparameter
description: Rufen Sie Daten mithilfe von Profilattributen innerhalb der Seite in [!DNL Target] ab.
title: Wie erhalte ich Daten mithilfe von In-Page-Profilattributen nach [!DNL Target] ?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%

---

# In-Page-Profilattribute

In-Page-Profilattribute in [!DNL Adobe Target] (auch &quot;In-mbox-Profilattribute&quot;genannt) sind Name/Wert-Paare, die direkt über den Seiten-Code übergeben werden und im Profil des Besuchers zur zukünftigen Verwendung gespeichert werden.

Die Profilattribute auf der Seite erlauben es, benutzerspezifische Daten im Profil von Target zu speichern, um sie später für ein Targeting gezielt zu segmentieren.

## Format

Profilattribute auf der Seite werden über einen Server-Aufruf als Name-Wert-Paar-Zeichenfolge mit dem Präfix &quot;profile&quot;an [!DNL Target] übergeben. vor dem Attributnamen an Target übergeben.

Attributnamen und -werte sind anpassbar (obwohl es einige „reservierte Namen“ für bestimmte Verwendungszwecke gibt).

Im Folgenden finden Sie einige Beispiele für In-Page-Profilattribute:

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## Anwendungsbeispiele

* **Anmeldeinformationen**: Geben Sie nicht personenbezogene Daten (non-PII) basierend auf der Anmeldung des Benutzers an [!DNL Target] weiter. Diese Daten können Mitgliedsstatus, Bestellverlauf oder mehr sein.
* **Store-Info:** verfolgen, welcher Store der bevorzugte Standort dieses Benutzers ist.
* **Bisherige Interaktionen**: verfolgen, was der Benutzer zuvor auf der Site getan hat, um die künftige Personalisierung vorzubereiten.

## Vorteile der Methode

Daten werden in Echtzeit an [!DNL Target] gesendet und können für denselben Server-Aufruf verwendet werden, bei dem die Daten eingehen.

## Einschränkungen

Erfordert Seiten-Code-Updates (direkt oder über ein Tag-Management-System).

Attribute und Werte sind in Server-Aufrufen sichtbar, sodass ein Besucher die Werte sehen kann. Wenn Informationen wie Kreditbereiche oder andere potenziell private Informationen freigegeben werden, ist diese Methode möglicherweise nicht der beste Ansatz.

## Codebeispiele

targetPageParamsAll (hängt die Attribute an alle Mbox-Aufrufe auf der Seite an):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams (hängt die Attribute an die globale Mbox auf der Seite an):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

Attribute im mboxCreate-Code:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## Links zu relevanten Informationen

[Profilattribute](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[Besucherprofil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
