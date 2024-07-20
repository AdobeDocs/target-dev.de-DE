---
title: Adobe Target Single Profile Update API
description: Erfahren Sie, wie Sie mit  [!DNL Adobe Target] [!UICONTROL Single Profile Update API] die Profildaten eines einzelnen Besuchers an  [!DNL Target] senden können.
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

Mit dem Wert [!DNL Adobe Target] [!UICONTROL Single Profile Update API] können Sie ein Profil-Update für einen einzelnen Benutzer senden. Der [!UICONTROL Single Profile Update API] ist fast identisch mit dem [!UICONTROL Bulk Profile Update API], aber ein Besucherprofil wird gleichzeitig aktualisiert, entsprechend dem API-Aufruf und nicht mit einer .cvs-Datei.

Der Wert [!UICONTROL Single Profile Update API] und wird im Allgemeinen verwendet, wenn eine Aktualisierung in Bezug auf eine Transaktion vorgenommen werden muss, die in einem Kanal stattfindet, der [!DNL Target] nicht implementiert hat. Sie möchten beispielsweise das Profil eines einzelnen Besuchers aktualisieren, der eine Offline-Aktion ausführt. Zu den Aktionen gehören das Erreichen eines Callcenters, die Finanzierung eines Darlehens, die Verwendung einer Treuekarte im Geschäft, der Zugriff auf einen Kiosk usw.

Zu den Vorteilen von [!UICONTROL Single Profile Update API] gehören:

* Keine Begrenzung der Anzahl der Profilattribute.
* Profilattribute, die über die Site gesendet werden, können über die API aktualisiert werden und umgekehrt.

## Einschränkungen 

* Der [!UICONTROL Single Profile Update API] ist auf die Durchführung von 1 Million Aktualisierungen in einem beliebigen rollierenden 24-Stunden-Zeitraum beschränkt.
* Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden.

  Wenn Sie weitere Aktualisierungen senden oder die Verarbeitung von Aktualisierungen in kürzeren Zeitrahmen erfordern, sollten Sie in Erwägung ziehen, Transaktionsprofilaktualisierungen über eine clientseitige Aktualisierung (empfohlen) oder über die serverseitige [!DNL Adobe Target] -API für die Bereitstellung[zu senden.](/help/dev/implement/delivery-api/overview.md)

* Die [!UICONTROL Single Profile Update API] ist eine Server-zu-Server-API und ist nicht für die Arbeit auf einer Webseite vorgesehen. Um ein Besucherprofil über Ihre Webseite zu aktualisieren, können Sie die Funktion [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) oder die [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md) verwenden.

## Format

Geben Sie die Profilparameter im Format `profile.paramName=value` an.

Um das Profil für einen `pcId` zu aktualisieren, verwenden Sie:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

Um das Profil für einen `mbox3rdPartyId` zu aktualisieren, verwenden Sie:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

Der [!UICONTROL Single Profile Update API] dient nur Updates. Wenn nichts gefunden wird, wird kein Profil erstellt.

## Hinweise

* Parameter und Werte müssen mit UTF-8 URL-kodiert werden.
* Das Parameterformat ist `profile.paramName`.
* Es müssen nicht alle Parameterwerte für alle pcIds und mbox3rdPartyIds vorhanden sein.
* Bei Parametern und Werten wird zwischen Groß- und Kleinschreibung unterschieden.
* Sowohl GET als auch POST werden unterstützt.
* Die aktuellen Größenbeschränkungen für Limit sind 8 KB für GET und 60 KB für POST.

## Antwort

Eine Beispielantwort für die oben genannten Anforderungen sieht wie folgt aus:

`trueRequest successfully submitted`

Diese Antwort gibt an, dass die Antwort gesendet wurde und bald verarbeitet wird.
