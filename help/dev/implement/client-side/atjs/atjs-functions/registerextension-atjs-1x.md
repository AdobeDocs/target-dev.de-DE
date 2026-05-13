---
keywords: registerExtension, registerExtension, registerExtension, at.js, Funktionen, Funktion, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: Verwenden Sie die [!UICONTROL registerExtension()]-Funktion für die  [!DNL Adobe Target] .js-JavaScript-Bibliothek , um eine bestimmte Erweiterung zu registrieren. (at.js 1.x)
title: Wie verwende ich die [!UICONTROL registerExtension()]?
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
TQID: https://experienceleague.adobe.com/qTWubp0dNesN-8vsooz8pdbjfSw1W1ktm-0bG6YRzJw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 63%

---

# [!UICONTROL registerExtension()] - at.js 1.x

Stellt eine Standardart zur Registrierung bestimmter Erweiterungen dar.

>[!NOTE]
>
>Diese Funktion ist nur für at.js-Versionen 1.*x* verfügbar. Diese Funktion wird seit der Veröffentlichung von at.js 2.*x* nicht mehr unterstützt. Diese Funktion gibt Standardinhalte zurück, wenn sie mit at.js 2.x verwendet wird.

Der Optionsparameter ist obligatorisch und hat die folgende Struktur:

| Schlüssel | Typ | Erforderlich | Beschreibung |
|--- |--- |--- |--- |
| name | Zeichenfolge | Ja | Name der Erweiterung |
| Module | Array[Zeichenfolge] | Ja | Ein Zeichenfolgen-Array, das die angefragten Modulnamen beschreibt |
| registrieren | Funktion | Ja | Eine Funktion zur Initialisierung und Erstellung der Erweiterung. Diese Funktion erhält, basierend auf dem Modul-Array, Argumente. |

Hinweise:

* Wird einer dieser Parameter nicht bereitgestellt, wird eine Ausnahme generiert.
* Ist das Modul-Array leer, wird eine Ausnahme generiert.

Weitere Informationen und Beispiele zur Verwendung von `[!UICONTROL registerExtension]` finden Sie auf der Seite [Adobe Experience Cloud Target atjs-Erweiterungen](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) auf GitHub.

## Methoden für Einstellungsmodule

| Schlüssel | Typ | Beschreibung |
|--- |--- |--- |
| clientCode | Zeichenfolge | Clientcode |
| serverDomain | Zeichenfolge | Edgeserverdomäne |
| globalMboxName | Zeichenfolge | Globaler Mbox-Name [!DNL Target] |
| globalMboxAutoCreate | Boolesch | Zeigt an, ob die automatische Erstellung aktiviert oder deaktiviert ist. |
| Zeitüberschreitung | Nummer | Zeitüberschreitung der Abfrage |

## Methoden für Logger-Module

| Schlüssel | Typ | Beschreibung |
|--- |--- |--- |
| log | Funktion | Protokolliert die Variablenliste der Argumente in der Browser-Konsole, falls vorhanden. Wird nur aktiviert, wenn `mboxDebug=true` an die URL übermittelt wird. |
| error | Funktion | Protokolliert die Variablenliste der Argumente in der Browser-Konsole. Wird nur aktiviert, wenn schwerwiegende Fehler auftreten, beispielsweise Zeitüberschreitungen des Netzwerks, nicht gefundene HTML-Knoten usw. |
