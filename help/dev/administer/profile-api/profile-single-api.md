---
title: Adobe Target Single Profile Update API
description: Verwendung von [!DNL Adobe Target] [!UICONTROL Single Profile Update API] , um die Profildaten eines einzelnen Besuchers an [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 6f7d9875e3b73352ead3a55e40a4b2f81f3d4400
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# [!DNL Adobe Target Single Profile Update API]

Die [!DNL Adobe Target] [!UICONTROL Single Profile Update API] ermöglicht den Versand einer Profilaktualisierung an einen einzelnen Benutzer. Die [!UICONTROL Single Profile Update API] und wird im Allgemeinen verwendet, wenn eine Aktualisierung für eine Transaktion vorgenommen werden muss, die in einem Kanal erfolgt, der nicht implementiert wurde [!DNL Target].

Die [!UICONTROL Single Profile Update API] ist auf die Durchführung von 1 Million Aktualisierungen in einem beliebigen rollierenden 24-Stunden-Zeitraum beschränkt. Aktualisierungen treten in der Regel in weniger als einer Stunde auf, können jedoch bis zu 24 Stunden dauern, bis sie angezeigt werden. Wenn Sie weitere Aktualisierungen senden oder die Verarbeitung von Aktualisierungen in kürzeren Zeitrahmen erfordern, sollten Sie in Erwägung ziehen, Transaktionsprofilaktualisierungen über eine clientseitige Aktualisierung (empfohlen) oder über die Variable [!DNL Adobe Target] serverseitig [Bereitstellungs-API](/help/dev/implement/delivery-api/overview.md).

Geben Sie die Profilparameter im Format an `profile.paramName=value`.

So aktualisieren Sie das Profil für eine `pcId`verwenden:

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

So aktualisieren Sie das Profil für eine `mbox3rdPartyId`verwenden:

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

Die [!UICONTROL Single Profile Update API] ist nur für Aktualisierungen vorgesehen. Wenn nichts gefunden wird, wird kein Profil erstellt.

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